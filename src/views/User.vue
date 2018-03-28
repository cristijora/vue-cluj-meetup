<template>
    <div>
        User
        {{$route.params.id}}
        <ul>
            <li v-for="post in posts" :key="post.id">
                {{post.title}}
            </li>
        </ul>
    </div>
</template>
<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        posts: []
      }
    },
    created() {
      axios.get('/posts',
        {
          params: {
            userId: this.$route.params.id
          }
        })
        .then(response => {
            this.posts = response.data;
        })
    }
  }
</script>
<style>
</style>