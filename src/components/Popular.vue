<script>
export  default {
    props: {
        info: {
            type: String,
            required: true,
        }
    },
    data() {
        return {
            flag: false,
        }
    },
    methods: {
        setNameFilms(el) {
        this.name = el.title
      }
    }
}
</script>

<template>
      <div v-for="el in info" class="card">
        <p :style="`background-image: url(${el.posterUrl})`" class="name"></p>
        <a @click="setNameFilms(el)" href="#" class="watch">WATCH</a>
      </div>
</template>

<style scoped>
@import url('../assets/app.css');
</style>