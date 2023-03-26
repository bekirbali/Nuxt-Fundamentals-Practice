<template>
  <h1>display weather of {{ this.data.name }}</h1>

  <div>
    <p>Temperature: {{ this.data?.main?.temp }}°C</p>
    <p>Feels like: {{ this.data?.main?.feels_like }}°C</p>
    <p>Humidity: {{ this.data?.main?.humidity }}%</p>
    <p>Wind speed: {{ this.data?.wind?.speed }}km/h</p>

    <img
      :src="`https://s3-us-west-2.amazonaws.com/s.cdpn.io/162656/${this.data?.weather[0].icon}.svg`"
      alt="icon"
    />
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
    },
  },
};
</script>
