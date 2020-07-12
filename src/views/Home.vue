<template>
  <div class="home-view-container">
    <h1>
      Welcome to Vue-a-Pet
    </h1>
    <p>If you want to adopt a new best friend,  click the button below to see the current pets we have at the center :)</p>
    {{ getAllCats.length }}
    Current number of animals: {{ animalsCount }}
    <br>
    <br>
    <button @click="togglePetForm" class="btn btn-primary">Add A Pet</button>

    <b-form @submit.prevent="handleSubmit" v-if="showPetForm">
        <b-form-group id="input-group-1" label="Pet's Name:" label-for="input-1">
          <b-form-input
            id="input-1"
            v-model="formData.name"
            required
            placeholder="Enter name"
          ></b-form-input>
        </b-form-group>

        <b-form-group id="input-group-2" label="Species:" label-for="input-2">
          <b-form-select
            id="input-2"
            v-model="formData.species"
            :options="['cats', 'dogs']"
            required
          ></b-form-select>
        </b-form-group>

        <b-form-group id="input-group-3" label="Pet's Age:" label-for="input-3">
          <b-form-input
            id="input-3"
            type="number"
            v-model="formData.age"
            required
            placeholder="Enter pet's age"
          ></b-form-input>
        </b-form-group>

        <b-button type="submit" variant="primary">Submit</b-button>
        <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
  </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  name: 'Home',
  data () {
    return {
      showPetForm: false,
      formData: {
        name: '',
        age: 0,
        species: null
      }
    }
  },
  computed: {
    ...mapGetters([
      'animalsCount',
      'getAllCats'
    ])
  },
  methods: {
    ...mapActions([
      'addPet'
    ]),
    togglePetForm () {
      this.showPetForm = !this.showPetForm
    },
    handleSubmit () {
      const { species, age, name } = this.formData
      const payload = {
        species,
        pet: {
          name,
          age
        }
      }
      this.addPet(payload)

      this.formData = {
        name: '',
        age: 0,
        species: null
      }
    }
  }
}
</script>
