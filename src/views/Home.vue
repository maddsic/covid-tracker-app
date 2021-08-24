<template>
  <main v-if="!loading" class="">
      <Title :text="title" :dataDate="dataDate" />

       <DisplayBoxes :stats='stats' />

       <SelectCountry @get-country="getCountryData" :countries="countries" />
  </main>

  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data
    </div>
    <img :src="loadingImage" alt="Loading Image" class="w-24 m-auto">
  </main>
</template>

<script>
// @ is an alias to /src

import Title from '@/components/Title'
import DisplayBoxes from '@/components/DisplayBoxes'
import SelectCountry from '@/components/SelectCountry'

export default {
  name: 'Home',
  components: {
    Title,
    DisplayBoxes,
    SelectCountry,
  },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/loadingsky.gif')
    }
  },
  methods: {
    async fetchData() {
      const res = await fetch("https://api.covid19api.com/summary")
      const data = await res.json()
      // console.log(data)
      return data
    },

  // getting single country data
    getCountryData(country) {
      this.stats = country
      this.title = country.Country
    },
  },
  // creating a lifecycle method called created which will load our data on DOM load
  async created () {
      const data = await this.fetchData()
      
      this.dataDate = data.Date
      this.stats = data.Global
      this.countries = data.Countries
      this.loading = false

},

}
</script>
