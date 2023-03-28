<template>
  <form @submit="submitHandler">
    <label for="city">Search</label>
    <input
      type="text"
      name="city"
      @change="searchText"
      v-model="search"
      placeholder="Search a city"
    />
    <button type="submit">Submit</button>
  </form>
  <DisplayWeatherData :data="weatherData" :forecastData="weatherForecast" />
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
      this.fetcher(this.search);
      this.search = "";
    },
    searchText(e) {
      this.search = e.target.value;
    },
  },
  props: {
    fetcher: Function,
    weatherData: Object,
    weatherForecast: Object,
  },
};
</script>

<style scoped lang="scss">
form {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  button {
    width: 50%;
    border: none;
    border-radius: 0.5rem;
    padding: 0.3rem;
    background-color: cadetblue;
    color: white;
    &:hover {
      background-color: rgb(90, 205, 190);
    }
    &:active {
      transform: translate(0.05px, 0.5px);

      background-color: rgb(73, 116, 117);
    }
  }
  input {
    padding: 0.3rem 0.5rem;
    border: none;
    border-radius: 0.5rem;
    text-transform: capitalize;
  }
}
</style>
