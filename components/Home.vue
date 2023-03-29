<template>
  <div v-if="loading">Loading...</div>
  <div class="home">
    <Form
      :fetcher="fetchData"
      :forecastFetcher="fetchForecastData"
      :weatherData="weatherData"
      :usersLocationWeatherData="usersLocationWeatherData"
      :dayOne="dayOne"
      :dayTwo="dayTwo"
      :dayThree="dayThree"
      :dayFour="dayFour"
      :dayFive="dayFive"
      v-if="!loading"
    />
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      title: "Hello World",
      show: true,
      apiKey: "6d8d685969d439d8178c3b7a901ebcf4",
      weatherData: [], // normal weather data
      // weatherForecast: [], // 5 days weather data
      usersLocationWeatherData: [], // weather data of user's location
      lat: "",
      lng: "",
      loading: true,
      dayOne: [],
      dayTwo: [],
      dayThree: [],
      dayFour: [],
      dayFive: [],
    };
  },
  methods: {
    async fetchData(city) {
      try {
        const { data } = await axios.get(
          `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${this.apiKey}`
        );
        this.weatherData = data;
        // console.log(this.weatherData, "weatherData");
      } catch (error) {
        console.log(error);
      } finally {
        this.loading = false;
      }
    },
    async fetchForecastData(city) {
      try {
        const { data } = await axios.get(
          `https://api.openweathermap.org/data/2.5/forecast/?q=${city}&units=metric&appid=${this.apiKey}`
        );
        console.log(this.weatherForecast, "forecast");
        this.weatherForecast = data;
        this.dayOne = this.weatherForecast.list.splice(0, 7);
        this.dayTwo = this.weatherForecast.list.splice(0, 7);
        this.dayThree = this.weatherForecast.list.splice(0, 7);
        this.dayFour = this.weatherForecast.list.splice(0, 7);
        this.dayFive = this.weatherForecast.list.splice(0, 7);

        console.log(this.weatherForecast.list, "list");
        console.log(this.dayThree, "dayOne");
      } catch (error) {
        console.log(error);
      } finally {
        this.loading = false;
      }
    },
    async fetchCurrentLocationWeather(position) {
      const { latitude, longitude } = position.coords;
      try {
        const { data } = await axios.get(
          `https://api.openweathermap.org/data/2.5/weather?lat=${latitude}&lon=${longitude}&units=metric&appid=${this.apiKey}`
        );
        this.usersLocationWeatherData = data;
        console.log(this.usersLocationWeatherData);
      } catch (error) {
        console.log(error);
      } finally {
        this.loading = false;
      }
    },
  },
  mounted() {
    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(
        this.fetchCurrentLocationWeather
      );
    } else {
      alert("Couldn't get your location info.");
      this.loading = false;
    }
  },
};
</script>

<style scoped lang="scss">
.home {
  .location {
    text-align: center;
    margin-top: 1rem;
    border: 1px solid red;
    padding: 1rem;
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
  }
}
</style>
