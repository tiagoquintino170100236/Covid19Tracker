<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />
    <DataBoxes :stats="stats" />
    <CountriesSelect @get-country="getCountryData" :countries="countries" />
    <div class="p-5">
      <button
        @click="clearCountryData"
        v-if="stats.Country"
        class="bg-green-700 text-white rounded p-3 mt-1 focus:outline-none hover:bg-green-600"
      >
        Clear Country
      </button>
    </div>
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data</div>
  </main>
</template>
<script>
import DataTitle from "@/components/DataTitle.vue"
import DataBoxes from "@/components/DataBoxes.vue"
import CountriesSelect from "@/components/CountriesSelect.vue"

export default {
  name: "CovidData",
  components: { DataTitle, DataBoxes, CountriesSelect },
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
    }
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary")
      const data = await res.json()
      return data
    },
    getCountryData(country) {
      this.stats = country
      this.title = country.Country
    },
    async clearCountryData() {
      this.loading = true
      const data = await this.fetchCovidData()
      this.title = "Global"
      this.stats = data.Global
      this.loading = false
    },
  },
  async created() {
    const data = await this.fetchCovidData()
    this.dataDate = data.Date
    this.stats = data.Global
    this.countries = data.Countries
    this.loading = false
    console.log(data)
  },
}
</script>
