<template>
    <div class="post">
        <RouterLink :to="{name: 'details', params: {id: post.id}}">
            <h3>{{ post.title }}</h3>
        </RouterLink>
        
        <p>{{ snippet }}</p>
       <!-- <RouterLink :to="{name: 'tag', params: {tag: post.tag}}"> -->
          <span v-for="tag in post.tags" :key="tag">
            #{{ tag }}
          </span>
        <!--</RouterLink> -->  
    </div>
</template>

<script>
import { computed } from "vue";

export default {
    props: ['post'],
    setup (props) {
      
        const snippet = computed(() => {
            return props.post.body.substring(0, 100) + '(...)'
        })

        return {snippet}
    }
}
</script>

<style>
  .post {
    margin: 0 40px 30px;
    padding-bottom: 30px;
    border-bottom: 1px dashed #e7e7e7;
  }
  .post h3 {
    display: inline-block;
    position: relative;
    font-size: 26px;
    color: white;
    margin-bottom: 10px;
    max-width: 400px;
  }
  .post h3::before {
    content: "";
    display: block;
    width: 100%;
    height: 100%;
    background: #068eb8;
    position: absolute;
    z-index: -1;
    padding-right: 40px;
    left: -30px;
    transform: rotateY(-1deg);
  }
  .post span {
    font-style: italic;
  }
</style>