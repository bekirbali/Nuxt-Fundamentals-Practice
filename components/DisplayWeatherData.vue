<template>
  <div v-if="this.forecastData?.city?.name">
    <h2>{{ forecastData?.city?.name }}</h2>
    <ul>
      <li v-for="forecast in forecastData.list" :key="forecast?.dt">
        <!-- {{ new Date(forecast?.dt * 1000).toLocaleDateString() }}: -->
        {{ forecast?.dt_txt }}
        {{ forecast?.main?.temp }}°C,
        {{ forecast?.weather?.map((desc) => desc.description) }}
      </li>
    </ul>
    <button @click="showIt">show forecast</button>
  </div>
  <div v-if="!this.forecastData?.city?.name" class="container">
    <p>City: {{ this.data?.name }}</p>
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
  },
  methods: {
    showIt() {
      console.log(this.forecastData);
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
  p {
    margin: 0;
  }
}
</style>
