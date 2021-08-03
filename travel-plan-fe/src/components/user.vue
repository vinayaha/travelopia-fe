<template>
    <div :class="['user']">
        <p>Name : {{ user.name }} </p>
        <p>Email : {{ user.email }} </p>
        <p>Country : {{ user.country }} </p>
        <p>Number Of Travellers : {{ user.numberOfTravellers }} </p>
        <p>Budget : ${{ user.budget }} </p>
    </div>
</template>

<style scoped>

.user {
  background: #e6e3e3;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

</style>

<script>
export default {
    name: "User",
    props:{
        user: Object,
    },
}
</script>