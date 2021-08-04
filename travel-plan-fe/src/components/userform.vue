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
        type="number"
      ></v-select>

      <v-text-field
        v-model="budget"
        label="Budget in $"
        required
        type="number"
      ></v-text-field>

      <v-btn
        :disabled="!valid"
        color="success"
        class="mr-4"
        @click="validate"
      >
        Submit
      </v-btn>
  
      <v-btn
        color="error"
        class="mr-4"
        @click="reset"
      >
        Reset Details
      </v-btn>
    </v-form>
  </v-app>
</template>

<style scoped>

</style>

<script>
import axios from 'axios'

export default {
  name: 'UserForm',
  data: () => ({
    valid: true,
    name: '',
    nameRules: [
      v => !!v || 'Name is required',
      v => (v && v.length <= 30) || 'Name must be less than 30 characters',
    ],
    email: '',
    emailRules: [
      v => !!v || 'E-mail is required',
      v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
    select: null,
    country: '',
    travellersCount: 0,
    budget: '',
    countries: ['India', 'Africa', 'Europe'],
    travellers: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15],
    checkbox: false,
    newUser: {}
  }),

  methods: {
    validate (e) {
      this.$refs.form.validate()
      if (!this.name && !this.email && !this.country && !this.numberOfTravellers && !this.budget) {
        alert("Please enter correct details")
      } else {
        this.newUser = {
          name: this.name,
          email: this.email,
          country: this.country,
          numberOfTravellers: parseInt(this.travellersCount),
          budget: parseInt(this.budget)
        }
        this.createObject(this.newUser).then(object => {
          this.newUser = object;
          console.log("POST JSON-Data : " + JSON.stringify(this.newUser));
          this.$emit('display-data', this.newUser)
        })
      }
    },
    reset () {
      this.$refs.form.reset()
    },
    createObject(Objects) {
      const input = Objects;
      console.log(JSON.stringify(input));
      return new Promise((resolve, reject) => {
        fetch(new Request('http://localhost:8080/traveller-plan/api/traveller'), {
          method: "POST",
          headers: {
            Accept: "application/json",
            "Content-Type": "application/json"
          },
          body: JSON.stringify(input)
        })
        .then(resp => {
          return resp.json();
        })
        .then(json =>{
          resolve(json);
        })
        .catch(err => {
          reject(err);
        })
      })
    }

  }
}
</script>