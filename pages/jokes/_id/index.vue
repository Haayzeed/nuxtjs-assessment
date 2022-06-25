<template>
    <div>
        <h2> {{joke.joke}} </h2>
        <hr>
        <small>Joke ID: {{$route.params.id}}</small>
    </div>
</template>
<script>
import axios from "axios"
export default {
    data() {
        return {
            joke: {}
        }
    },
    created() {
        axios.get(`https://icanhazdadjoke.com/j/${this.$route.params.id}`, {
        headers: {
          accept: 'application/json',
        },
      }).then((response) => {
        console.log(response.data)
        this.joke = response.data;
      })
    }
}
</script>