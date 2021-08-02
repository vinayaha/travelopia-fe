<template>
    <h1> {{ title }}</h1>
</template>

<style scoped>

</style>

<script>
export default {
    name: 'header',
    props: {
        title: String,
    }
}
</script>