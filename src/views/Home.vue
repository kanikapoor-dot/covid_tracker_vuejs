<template>
  <main v-if="!loading">
    <DataTitle :text="title" :dataDate="dataDate" />

    <DataBoxes :stats="stats" />

    <CountrySelect @get-country="getCountryData" :countries="countries" />

    <button
      @click="clearCountryData"
      v-if="stats.Country"
      class="
        bg-green-700
        text-white
        rounded
        mb-4
        p-3
        mt-10
        focus:outline-none
        hover:bg-green-600
      "
    >
      Global Data
    </button>
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <img :src="loadingImage" class="w-24 m-auto" />
  </main>
</template>

<script>
import DataTitle from "@/components/DataTitle.vue";
import DataBoxes from "@/components/DataBoxes.vue";
import CountrySelect from "@/components/CountrySelect.vue";

export default {
  name: "Home",
  components: {
    DataTitle,
    DataBoxes,
    CountrySelect,
  },
  data() {
    return {
      loading: true,
      dataDate: "",
      title: "Globel",
      stats: {},
      countries: [],
      loadingImage: require("../assets/Coronavirus.gif"),
    };
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch("https://api.covid19api.com/summary", 
      // {
      //   method: "GET",
      //   mode: "no-cors",
      //   headers: {
      //     Accept: "application/json",
      //   },
      // }
      );
      const data = await res.json();
      return data;
    },
    getCountryData(country) {
      this.stats = country;
      this.title = country.Country;
    },
    async clearCountryData() {
      this.loading = true;
      const data = await this.fetchCovidData();
      this.title = "Global";
      this.stats = data.Global;
      this.dataDate = data.Date;
      this.countries = data.Countries;
      this.loading = false;
    },
  },
  async created() {
    const data = await this.fetchCovidData();
    console.log(data);
    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
};
</script>
