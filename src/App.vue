<template>
  <div>
    <h1>Countries</h1>
    <div class="main-container">
      <!-- <countries-list v-bind:countries='countries'></countries-list> -->
      <countries-search v-bind:countries='countries'></countries-search>
      <!-- <country-dropdown v-bind:countries='countries'></country-dropdown> -->
      <country-detail v-bind:country='selectedCountry'></country-detail>
    </div>
  </div>
</template>

<script>
import CountriesList from './components/CountriesList.vue';
import { eventBus } from './main.js'
import CountryDetail from './components/countryDetail.vue';
import CountryDropdown from './components/CountryDropdown.vue'
import CountriesSearch from './components/countriesSearch.vue'

export default {
  name: 'app',
  data(){
    return {
      countries: [],
      selectedCountry: null,
    }
  },
  mounted(){
    fetch('https://restcountries.eu/rest/v2/all')
    .then(res => res.json())
    .then(countries => this.countries = countries)

    eventBus.$on('country-selected', (country) =>{
      this.selectedCountry = country
    })
  },

  components: {
    "countries-list": CountriesList,
    "country-detail": CountryDetail,
    "country-dropdown": CountryDropdown,
    "countries-search": CountriesSearch
  }
}
</script>

<style>
  .main-container {
    display: flex;
    justify-content: space-between;
  }
</style>
