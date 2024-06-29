<script>
import Popular from './components/Popular.vue';
import Button from './components/button.vue'

import axios from 'axios'

  export default {
    components: {
      Button,
      Popular,
    },
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
    },
  }
</script>

<template>
  <header class="header">
    <div class="search">
        <h3>Search of FILMS</h3>
        <div class="form1">
          <input v-model="name" class="input" type="text" placeholder="search">
          <Button :name="String('GET')" @click="getPlayersOnName"/>
        </div>
        <div class="form2">
          <Button @click="getSourseApiPopular" :name="String('POPULAR')"/>
        </div>
    </div>
  </header>
  <main class="main">
    <div v-if="flagPopular == true" class="cards">
      <Popular :info="info"/>
      <!-- <div v-for="el in info" class="card">
        <p :style="`background-image: url(${el.posterUrl})`" class="name"></p>
        <a @click="setNameFilms(el)" href="#" class="watch">WATCH</a>
      </div> -->
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
