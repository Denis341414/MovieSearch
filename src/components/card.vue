<script>
export default {
    props: {
        posterURL: {
            type: String,
            required: true,
        }
    }
}
</script>

<template>
    <div class="card">
        <p :style="`background-image: url(${posterURL})`" class="name"></p>
        <a @click="" href="#" class="watch">WATCH</a>
    </div>
</template>

<style scoped>
@import url('../assets/app.css');
</style>