<template>
  <div class="home">
    <Hero />
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Home',
  data() {
    return {
      movies: [],
    }
  },
  async fetch() {
    await this.getMovies()
  },
  methods: {
    async getMovies() {
      let self = this
      await axios
        .get(
          `https://api.themoviedb.org/3/movie/now_playing?api_key=68d7df918961fa60932d659428111f16&language=en-US&page=1`
        )
        .then((res) => {
          res.data.results.forEach((movie) => {
            self.movies.push(movie)
          })
        })
        .catch((err) => {
          console.log(err)
        })
        .finally(() => {
          console.log('Get 20 movies')
        })
    },
  },
}
</script>
