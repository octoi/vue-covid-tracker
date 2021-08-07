<template>
  <div class="home">Hello World</div>
</template>

<script>
export default {
  name: "Home",
  components: {},
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
    console.log(data);
  },
};
</script>
