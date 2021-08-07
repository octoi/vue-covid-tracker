<template>
  <main v-if="!loading">
    <DataTitle :dataDate="dataDate" :text="title" />
  </main>

  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data ...
      <img :src="loadingImage" class="w-24 m-auto" alt="Loading..." />
    </div>
  </main>
</template>

<script>
import DataTitle from "@/components/DataTitle";

export default {
  name: "Home",
  components: {
    DataTitle,
  },
  data() {
    return {
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: require("../assets/hourglass.gif"),
    };
  },
  methods: {
    async fetchCovidData() {
      const request = await fetch("https://api.covid19api.com/summary");
      const data = await request.json();
      return data;
    },
  },
  async created() {
    const data = await this.fetchCovidData();

    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },
};
</script>
