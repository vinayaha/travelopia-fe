<template>
    <div>
        <div :key="user.id" v-for="user in users">
            <User :user="user" />
        </div>
         <button @click="onClick()" :style="{ background: 'black' }" class="btn">
            Back
        </button>
    </div>
</template>

<style scoped>
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>

<script>
import User from './user.vue'

export default {
    name: "DisplayUser",
    components: {
        User,
    },
    props: {
        "users":Array
    },
    data() {
        return {
            name:'',
            email:'',
            country:''
        }
    },
    methods: {
        onClick() {
            this.$emit('btn-click')
        },
    }
}
</script>