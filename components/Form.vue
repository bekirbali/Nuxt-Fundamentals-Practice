<template>
  <form @submit="submitHandler">
    <label for="city">Search</label>
    <input type="text" name="city" @change="searchText" v-model="search" />
    <button type="submit">Submit</button>
  </form>
  <DisplayWeatherData :data="weatherData" />
</template>

<script>
export default {
  data() {
    return {
      search: "",
    };
  },
  methods: {
    submitHandler(e) {
      e.preventDefault();
      const { data } = this.fetcher(this.search);

      this.search = "";
    },
    searchText(e) {
      this.search = e.target.value;
      console.log(this.search);
    },
  },
  props: {
    fetcher: Function,
    weatherData: Array,
  },
};
</script>
