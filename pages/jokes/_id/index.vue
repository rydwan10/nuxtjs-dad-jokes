<template>
  <div>
    <nuxt-link to="/jokes">Bact To Jokes</nuxt-link>
      <h2>{{ joke }}</h2>
      <br>
      <hr>
      <p>Joke ID: {{ $route.params.id }}</p>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  data(){
    return {
      joke: {}
    }
  },
  async created(){
       const config = {
            headers: {
                Accept: "application/json",
            }
        }
        try {
            const res = await axios.get(`https://icanhazdadjoke.com/j/${this.$route.params.id}`, config);
            
            // this.jokes = res.data.results;
            this.joke = res.data.joke;
        } catch (err) {
            console.log(err);
        }
  },
  head() {
    return {
      title: this.joke,
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Best place for corny dad jokes"
        }
      ]
    }
  }
}
</script>

<style>

</style>