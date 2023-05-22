<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <input type="text" v-model="city" @keyup.enter="getWeather">
    <p>Temperature: {{ temperature }}°C</p>
    <img :src="iconUrl" alt="Weather icon">
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      title: 'Weather App',
      city: 'London',
      temperature: null,
      iconUrl: null
    }
  },
  methods: {
    getWeather() {
      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=YOUR_API_KEY&units=metric`)
        .then(response => {
          this.temperature = response.data.main.temp;
          this.iconUrl = `http://openweathermap.org/img/w/${response.data.weather[0].icon}.png`;
        });
    }
  },
  mounted() {
    this.getWeather();
  }
}
</script>
