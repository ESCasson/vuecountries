<template lang="html">
  <div>
    <label for="countries-search">Enter the country name:</label>
    <input type="text" v-model="enteredLetters">
    <ul>
      <country-item v-for="(country, index) in countries" v-bind:country="country" v-bind:key="index"
        v-if="(country.name.indexOf(enteredLetters)!==-1)"></country-item>
    </ul>


  </div>
</template>

<script>
import { eventBus } from '../main.js'

import CountryItem from './CountryItem.vue';

export default {
  name: "countries-search",
  data() {
    return {enteredLetters: null
  }},
  props: ["countries"],
  methods: {
    handleChange : function (){
      eventBus.$emit('country-selected', this.countryChoice)

    }
  },
  components: {
    "country-item" : CountryItem
  }
}
</script>

<style lang="css" scoped>
</style>
