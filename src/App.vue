<script>
  import axios from 'axios'
  
  export default {
    
    data() {
      return {
        flagPopular: false,
        flagWatch: false,
        flagStoped: false,
        info: '',
        name: '',
        posterThichElementUrl: '',
        urlElement: '',
        
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
        })
      },
      getPlayersOnName() {
        this.flagPopular = false
        this.flagWatch = true
        axios.get(`https://kinobox.tv/api/players?title=${this.name}`)
        .then(res => {
          console.log(res)
          return res.data
        })
        .then(data => {
          if (data[0].iframeUrl != null) this.urlElement = data[0].iframeUrl
          else if (data[1].iframeUrl != null) this.urlElement = data[1].iframeUrl
          else if (data[2].iframeUrl != null) this.urlElement = data[2].iframeUrl
        })


        axios.get('https://kinobox.tv/api/films/popular?type=film')
        .then(result => {
          return result.data
        })
        .then(data => {
          for (let i = 0; i < data.length; i++) {
            if (data[i].title == this.name) {
              this.posterThichElementUrl = data[i].posterUrl
              this.flagPopular = false
              this.flagWatch = false
              this.flagStoped = true
              console.log()
            }
          }
        })

      },
      setNameFilms(el) {
        this.name = el.title
      }
    },
  }
</script>

<template>
  <header class="header">
    <div class="search">
        <h3>Search of FILMS</h3>
        <div class="form1">
          <input v-model="name" class="input" type="text" placeholder="search">
          <button @click="getPlayersOnName" class="get">GET</button>
        </div>
        <div class="form2">
          <button @click="getSourseApiPopular" class="popular">POPULAR</button>
        </div>
    </div>
  </header>
  <main class="main">
    <div v-if="flagPopular == true" class="cards">
      <div v-for="el in info" class="card">
        <p :style="`background-image: url(${el.posterUrl})`" class="name"></p>
        <a @click="setNameFilms(el)" href="#" class="watch">WATCH</a>
      </div>
    </div>

    <div v-else-if="flagWatch == true" class="cards">
      <div class="card">
        <p :style="`background-image: url(${posterThichElementUrl})`" class="name"></p>
        <a @click="" href="#" class="watch">WATCH</a>
      </div>
    </div>

    <div v-else-if="flagStoped == true" class="cards">
      <div class="card">
        <p :style="`background-image: url(${posterThichElementUrl})`" class="name"></p>
        <a @click="" :href="urlElement" class="watch">WATCH</a>
      </div>
    </div>
  </main> 
</template>

<style scoped>
/* header */
  @import url('./assets/app.css');
</style>
