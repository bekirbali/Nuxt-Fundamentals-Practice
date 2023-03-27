<template>
  <div>
    <Form :fetcher="fetchData" :weatherData="weatherData" />
  </div>
</template>

<script>
import axios from "axios";
import "./App.scss";
export default {
  data() {
    return {
      title: "Hello World",
      show: true,
      apiKey: "6d8d685969d439d8178c3b7a901ebcf4",
      weatherData: [],
    };
  },
  methods: {
    showToggle() {
      this.show = !this.show;
    },
    // submitHandler(e) {
    //   e.preventDefault();
    //   this.fetchData();
    // },
    // searchText(e) {
    //   this.search = e.target.value;
    //   console.log(this.search);
    // },
    async fetchData(city) {
      const { data } = await axios.get(
        `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${this.apiKey}`
      );
      this.weatherData = data;
      console.log(this.weatherData);
    },
  },
};
</script>
