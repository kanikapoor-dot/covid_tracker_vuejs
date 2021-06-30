<template>
  <select
    @change="onChange()"
    v-model="selected"
    name="country"
    id="country"
    class="form-select block mt-10 w-full border p-3 rounded bg-yellow-50"
  >
    <option value="0">Select Country</option>
    <option v-for="country in countries" :value="country.ID">
      {{ country.Country }}
    </option>
  </select>
</template>

<script>
export default {
  name: "CountrySelect",
  props: ["countries"],
  data() {
    return {
      selected: 0,
    };
  },
  methods: {
    onChange() {
      const country = this.countries.find((item) => item.ID === this.selected);
      this.$emit("get-country", country);
    },
  },
};
</script>
