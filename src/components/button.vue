<script>
export default {
    props: {
        name: {
            type: String,
            required: true
        }
    },
    data() {
        return {
            
        }
    },
}
</script>

<template>
    <button class="get">{{ name }}</button>
</template>

<style scoped>
@import url('../assets/app.css');
</style>