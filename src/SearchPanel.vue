<template>
  <div class="p-4 md:p-12 text-center lg:text-left">
    <!-- Image for mobile view-->
    <div :style="`background-image: url(${$parent.movie.Poster})`"
         class="block lg:hidden rounded-br shadow-xl mx-auto -mt-16 h-48 w-48 bg-cover bg-center"></div>

    <h1 class="text-3xl font-bold pt-8 lg:pt-0">Search a movie</h1>
    <div>
      <input class="shadow-sm p-4 px-0 border-b my-6 font-semibold text-2xl" placeholder="Movie name" type="text" v-model="search"/>
    </div>
    <slot />
  </div>
</template>
<script>
export default {
  name: 'SearchPanel',
  data () {
    return {
      search: null,
    }
  },
  watch: {
    search (value) {
      this.$emit('search', value)
    },
  },
  inject: ['movie']
}
</script>
