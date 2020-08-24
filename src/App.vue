<template>
  <div class="max-w-4xl flex items-center h-auto lg:h-screen flex-wrap mx-auto my-32 lg:my-0">

    <!--Main Col-->
    <div
        class="w-full lg:w-3/5 rounded-lg lg:rounded-l-lg lg:rounded-r-none shadow-2xl bg-white opacity-75 mx-6 lg:mx-0"
        id="profile">
      <SearchPanel @search="handleSearch" v-model="search">
        <a :href="`https://www.imdb.com/title/${movie.imdbID}`" class="font-bold text-gray-600 underline"
           target="_blank" v-if="movie.imdbID">See
          more on IMDB</a>
      </SearchPanel>

    </div>

    <!--Img Col-->
    <div class="w-full lg:w-2/5">
      <!-- Big profile image for side bar (desktop) -->
      <img :src="movie.Poster" class="rounded-none lg:rounded-lg shadow-2xl hidden lg:block">
      <!-- Image from: http://unsplash.com/photos/MP0IUfwrn0A -->
    </div>
  </div>
</template>

<script>
import SearchPanel from './SearchPanel.vue'

export default {
  name: 'App',
  components: {
    SearchPanel,
  },
  data () {
    return {
      search: null,
      movie: {
        Poster: 'https://picsum.photos/id/1/400/600',
        Title: null,
        Year: null,
        imdbID: null,
      },
    }
  },
  watch: {
    search (value) {
      const API_KEY = 'a5549d08'
      const MOVIE_API_URL = `https://www.omdbapi.com/?s=${value}&apikey=${API_KEY}`

      this.loading = true

      fetch(MOVIE_API_URL).then(response => response.json()).then(jsonResponse => {
        this.movie = jsonResponse.Search ? Object.values(jsonResponse.Search)[0] : this.movie
        console.log(this.movie)
        this.loading = false
      })
    },
  },
  methods: {
    handleSearch (searched) {
      this.search = searched
    },
  },
}
</script>
