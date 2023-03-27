<template>
  <div v-show="this?.data?.name" class="container">
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

    <button @click="showIcon">show icon</button>
  </div>
</template>

<script>
export default {
  props: {
    data: Object,
  },
};
</script>

<!--   :src="`https://s3-us-west-2.amazonaws.com/s.cdpn.io/162656/${this.data?.weather[0].icon}.svg`" -->

<!-- <img :src="`../assets/icons/${this.icon}.svg`" alt="icon" /> -->

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
