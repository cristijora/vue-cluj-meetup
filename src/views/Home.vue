<template>
    <div>
        <h1>Search</h1>
        <input type="text" v-model="searchValue">
        <button @click="search">
            Search
        </button>
        <ul>
            <li v-for="user in users" :key="user.id">
                <router-link
                        :to="{name: 'user', params: {id:user.id}}">
                    {{user.name}}
                </router-link>
            </li>
        </ul>
    </div>
</template>
<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        searchValue: '',
        users: [],
        imageSource: 'https://avatars0.githubusercontent.com/u/210?v=4'
      }
    },
    methods: {
      search(evt) {
        let url = '/users'
        axios.get(url, {
          params: {
            q: this.searchValue
          }
        }).then((response) => {
          this.users = response.data;
        })
      }
    }
  }

</script>

<style lang="scss">
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
    }

    #nav {
        padding: 30px;
        a {
            font-weight: bold;
            color: #2c3e50;
            &.router-link-exact-active {
                color: #42b983;
            }
        }
    }
</style>
