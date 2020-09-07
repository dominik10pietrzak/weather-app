<template>
  <div class="main">
    <div class="top">
      <div class="background" v-if="weather">
        <img
          v-if="time < 21 && time > 6"
          v-bind:src="require(`../../assets/${weather.description}.jpg`)"
        />
        <img
          v-else
          v-bind:src="require(`../../assets/night/${weather.description}.jpg`)"
          class="background"
        />
      </div>
      <div class="left">
        <h1 class="temp">{{Math.round(weather.currentTemp)}}&#xb0;</h1>
        <h3 class="description">{{weather.description}}</h3>
        <div class="details">
          <span>
            Humidity
            <br />
            {{weather.humidity}} %
          </span>
          <div class="line"></div>
          <span>
            Wind
            <br />
            {{Math.round(weather.windSpeed)}} KM/H
          </span>
        </div>
      </div>
      <div class="right">
        <h1>{{weather.city}}</h1>
        <div class="line"></div>
      </div>
    </div>
    <Forecast :weather="weather" />
  </div>
</template>

<script>
import Forecast from "../forecast/Forecast.vue";

export default {
  name: "Main",
  props: ["weather"],
  data() {
    return {
      time: "",
    };
  },
  components: {
    Forecast,
  },
  mounted() {
    const date = new Date();
    const hour = date.getHours();
    this.time = hour;
    console.log(this.time);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
@import "./main.scss";
</style>
