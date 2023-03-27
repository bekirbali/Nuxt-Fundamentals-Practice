<template>
  <div class="home">
    <Form
      :fetcher="fetchData"
      :weatherData="weatherData"
      :currentWeatherData="currentWeatherData"
      :locationFetcher="fetchCurrentLocationWeather"
    />
    <div class="location">
      <h3 for="">Show me the weather of my city.</h3>
      <button v-if="show" @click="fetchCurrentLocationWeather">Show</button>
    </div>
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
      weatherData: [],
      currentWeatherData: [],
      lat: "",
      lng: "",
    };
  },
  methods: {
    async fetchData(city) {
      const { data } = await axios.get(
        `https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=${this.apiKey}`
      );
      this.weatherData = data;
    },
    async fetchCurrentLocationWeather() {
      const { data } = await axios.get(
        `https://api.openweathermap.org/data/2.5/weather?lat=${this.lat}&lon=${this.lng}&units=metric&appid=${this.apiKey}`
      );
      this.weatherData = data;
      this.show = false;
    },
    async getLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition((position) => {
          this.lat = position.coords.latitude.toString();
          this.lng = position.coords.longitude.toString();
        });
      } else {
        alert("Couldn't get your location info.");
      }
    },
  },
  beforeMount() {
    this.getLocation();
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
