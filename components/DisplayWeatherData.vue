<template>
  <div v-if="!this.data?.name"></div>
  <div v-if="this?.data?.name" class="container">
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
  props: {
    data: Object,
    locationData: Object,
    locationFetcher: Function,
  },
  // mounted() {
  //   this.locationFetcher();
  // },
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
