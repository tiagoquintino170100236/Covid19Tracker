<template>
  <div id="app">
    <Header></Header>
    <CovidData></CovidData>
  </div>
</template>

<script>
import Header from "./components/Header.vue"
import CovidData from "@/components/CovidData.vue"

export default {
  name: "App",
  components: {
    Header,
    CovidData,
  },
}
</script>
