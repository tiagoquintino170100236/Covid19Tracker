<template>
  <div class="p-5">
    <select
      @change="onChange()"
      v-model="selected"
      class="form-select mt-2 block w-full border p-3 rounded"
    >
      <option value="0">Select Country</option>
      <option
        v-for="country in countries"
        :key="country.ID"
        :value="country.ID"
      >
        {{ country.Country }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "CountriesSelect",
  props: ["countries"],
  data() {
    return {
      selected: 0,
    }
  },
  methods: {
    onChange() {
      const country = this.countries.find((item) => item.ID === this.selected)

      this.$emit("get-country", country)
    },
  },
}
</script>
