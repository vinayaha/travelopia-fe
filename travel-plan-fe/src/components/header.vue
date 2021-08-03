<template>
    <div>
        <h1> {{ title }}</h1>
        <h3> Enter your plan details </h3>
    </div>
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