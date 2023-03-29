<template>
  <div v-if="this.data?.name" class="container">
    <p>City: {{ this.data?.name }}</p>
    <h3>{{ this.data.weather[0].description }}</h3>
    <p>Temperature: {{ this.data?.main?.temp }}°C</p>
    <p>Feels like: {{ this.data?.main?.feels_like }}°C</p>
    <p>Humidity: {{ this.data?.main?.humidity }}%</p>
    <p>Wind speed: {{ this.data?.wind?.speed }}km/h</p>

    <img
      :src="`../icons/${this.data?.weather?.map(
        (weather) => weather.icon
      )}.svg`"
      alt="icon"
    />
    <div class="forecast">
      <div>
        <p v-for="day in dayOne">
          {{ day.dt_txt }}
        </p>
      </div>
      <div>
        <p v-for="day in dayTwo">
          {{ day.dt_txt }}
        </p>
      </div>
      <div>
        <p v-for="day in dayThree">
          {{ day.dt_txt }}
        </p>
      </div>
      <div>
        <p v-for="day in dayFour">
          {{ day.dt_txt }}
        </p>
      </div>
      <div>
        <p v-for="day in dayFive">
          {{ day.dt_txt }}
        </p>
      </div>
    </div>
    <button @click="showIt">show forecast</button>
  </div>
  <div v-if="!this.data?.name" class="container">
    <p>City: {{ this.locationWeatherData?.name }}</p>
    <p>Temperature: {{ this.locationWeatherData?.main?.temp }}°C</p>
    <p>Feels like: {{ this.locationWeatherData?.main?.feels_like }}°C</p>
    <p>Humidity: {{ this.locationWeatherData?.main?.humidity }}%</p>
    <p>Wind speed: {{ this.locationWeatherData?.wind?.speed }}km/h</p>

    <img
      :src="`../icons/${this.locationWeatherData?.weather?.map(
        (weather) => weather.icon
      )}.svg`"
      alt="icon"
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      dates: [],
    };
  },
  props: {
    data: Object,
    forecastData: Object,
    hourlyData: Object,
    locationWeatherData: Object,
    splitDays: Array,
    loading: Boolean,
    dayOne: Array,
    dayTwo: Array,
    dayThree: Array,
    dayFour: Array,
    dayFive: Array,
  },
  methods: {
    showIt() {
      const day = this.forecastData?.list.splice(0, 7);
      return day;
    },
  },
};
</script>

<style scoped lang="scss">
.container {
  margin-top: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  img {
    width: 100px;
  }
  p {
    margin: 0;
  }
  .forecast {
    display: flex;
    gap: 1rem;
  }
}
</style>
