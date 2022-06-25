<template>
  <div>
    <form @keypress="searchJokes">
        <input v-model="text" type="text">
    </form>
    <div v-for="joke in jokes" :key="joke.id" class="jokes">
      <nuxt-link :to="'jokes/' + joke.id">
        {{ joke.joke }}
      </nuxt-link>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  // name: "JokesIndexPage"
  data() {
    return {
      jokes: [],
      text: ""
    }
  },
  created() {
    this.fetchJokes();
  },
  methods: {
    fetchJokes() {
        axios
      .get('https://icanhazdadjoke.com/search', {
        headers: {
          accept: 'application/json',
        },
      })
      .then((response) => {
        this.jokes = response.data.results
      })
    },
    searchJokes() {
    axios
      .get(`https://icanhazdadjoke.com/search?term=${this.text}`, {
        headers: {
          accept: 'application/json',
        },
      })
      .then((response) => {
        this.jokes = response.data.results
      })
    }
  },
}
</script>
<style scoped>
.jokes {
  border: 1px solid #eee;
  padding: 10px;
}
</style>
