<template>
  <div class="home">
    <!--$event é o argumento(by) passado no customEvent, contendo o parametro passado na function 'updateFilter' @click -->
    <FilterNav :filter="filter" @changeFilter="filter = $event"/>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete"/>
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '@/components/SingleProject.vue'
import FilterNav from '@/components/FilterNav.vue'

export default {
  name: 'HomeView',
  components: {SingleProject, FilterNav},
  data() {
    return {
      projects: [], 
      filter: 'all'
    }
  },
  mounted(){
    fetch('http://localhost:3000/project')
    .then(res => res.json())
    .then(data => this.projects = data)
    .catch(err => console.log(err.message))
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((proj) => {
        return proj.id !== id
      })
    },
    handleComplete(id) {
      const p = this.projects.find((proj) => {
        return proj.id === id
      })
      p.complete = !p.complete
    }
  },
  computed: {
    filteredProjects() {
      if(this.filter === 'completed') {
        return this.projects.filter(project => project.complete)
      } 
      if(this.filter === 'ongoing') {
        return this.projects.filter(proj => !proj.complete)
      }

    return this.projects

    }
  }
}
</script>
