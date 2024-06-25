<script>
  import axios from 'axios'
  import Search from './components/Search.vue'

  export default {
    components: {

    },
    data() {
      return {
        flagPopular: false,
        flagWatch: false,
        info: '',
      }
    },
    methods: {
      getSourseApiPopular() {
        this.flagPopular = true
        this.flagWatch = false
        axios.get('https://kinobox.tv/api/films/popular?type=film')
        .then(res => {
          this.info = res.data
          console.log(this.info)
          console.log(this.info[0].posterUrl)
        }).catch(console.error('ddd'))
      },
    }
  }
</script>

<template>
  <header class="header">
    <div class="search">
        <h3>Search of FILMS</h3>
        <Search/>
        <div class="form2">
          <button @click="getSourseApiPopular" class="popular">POPULAR</button>
        </div>
    </div>
  </header>
  <main class="main">
    <div v-if="flagPopular == true" class="cards">
      <div v-for="el in info" class="card">
        <!-- <div :style="`background-image: url(${el.posterUrl})`" class="img">asdas</div> -->
        <p :style="`background-image: url(${el.posterUrl})`" class="name"></p>
        <a href="#" class="watch">WATCH</a>
      </div>
    </div>
  </main> 
</template>

<style scoped>
/* header */
  @import url('./assets/app.css');
</style>
