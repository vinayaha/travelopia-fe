<template>
<v-app id="inspire">
    <v-form
      ref="form"
      v-model="valid"
      lazy-validation
    >
      <v-text-field
        v-model="name"
        :counter="10"
        :rules="nameRules"
        label="Name"
        required
      ></v-text-field>
  
      <v-text-field
        v-model="email"
        :rules="emailRules"
        label="E-mail"
        required
      ></v-text-field>
  
      <v-select
        v-model="country"
        :items="countries"
        :rules="[v => !!v || 'Country is required']"
        label="Where do you want to go?"
        required
      ></v-select>

      <v-select
        v-model="travellersCount"
        :items="travellers"
        :rules="[v => !!v || 'traveller count is required']"
        label="Number of travellers?"
        required
      ></v-select>

      <v-text-field
        v-model="budget"
        label="Budget"
        required
      ></v-text-field>

      <v-btn
        :disabled="!valid"
        color="success"
        class="mr-4"
        @click="validate"
      >
        Validate
      </v-btn>
  
      <v-btn
        color="error"
        class="mr-4"
        @click="reset"
      >
        Reset Form
      </v-btn>
    </v-form>
  </v-app>
</template>

<style scoped>

</style>

<script>
export default {
  name: 'UserForm',
  data: () => ({
    valid: true,
    name: '',
    nameRules: [
      v => !!v || 'Name is required',
      v => (v && v.length <= 10) || 'Name must be less than 10 characters',
    ],
    email: '',
    emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
    select: null,
    country: '',
    travellersCount: 0,
    budget: 0,
    countries: ['India', 'Africa', 'Europe'],
    travellers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10],
    checkbox: false,
  }),

  methods: {
    validate () {
      this.$refs.form.validate()
      console.log("Inside Validate")
    },
    reset () {
      this.$refs.form.reset()
      console.log("Inside Reset")
    },
  },
}
</script>