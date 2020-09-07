<template>
  <div class="forecast">
    <div class="container">
      <div class="child">
        <h2>{{daysOfWeek[0]}}</h2>
        <img
          v-if="weather"
          v-bind:src="require(`../../assets/weather-images/${weather.descIn1D}.png`)"
        />
        <h3>{{Math.round(weather.tempIn1D)}}&#xb0;</h3>
        <span>{{weather.descIn1D}}</span>
      </div>
      <div class="child">
        <h2>{{daysOfWeek[1]}}</h2>
        <img
          v-if="weather"
          v-bind:src="require(`../../assets/weather-images/${weather.descIn2D}.png`)"
        />
        <h3>{{Math.round(weather.tempIn2D)}}&#xb0;</h3>
        <span>{{weather.descIn2D}}</span>
      </div>
      <div class="child">
        <h2>{{daysOfWeek[2]}}</h2>
        <img
          v-if="weather"
          v-bind:src="require(`../../assets/weather-images/${weather.descIn3D}.png`)"
        />
        <h3>{{Math.round(weather.tempIn3D)}}&#xb0;</h3>
        <span>{{weather.descIn3D}}</span>
      </div>
      <div class="child">
        <h2>{{daysOfWeek[3]}}</h2>
        <img
          v-if="weather"
          v-bind:src="require(`../../assets/weather-images/${weather.descIn4D}.png`)"
        />
        <h3>{{Math.round(weather.tempIn4D)}}&#xb0;</h3>
        <span>{{weather.descIn4D}}</span>
      </div>
      <div class="child">
        <h2>{{daysOfWeek[4]}}</h2>
        <img
          v-if="weather"
          v-bind:src="require(`../../assets/weather-images/${weather.descIn5D}.png`)"
        />
        <h3>{{Math.round(weather.tempIn5D)}}&#xb0;</h3>
        <span>{{weather.descIn5D}}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Forecast",
  props: ["weather"],
  data() {
    return {
      daysOfWeek: [],
    };
  },
  mounted() {
    const date = new Date();
    const day = date.getDay();
    console.log(day);

    const days = ["SUN", "MON", "TUE", "WED", "THU", "FRI", "SAT"];

    let idx = day + 1;
    for (let i = 0; i < 5; i++) {
      if (idx === 6) {
        idx = 0;
        this.daysOfWeek.push(days[idx]);
      } else {
        this.daysOfWeek.push(days[idx]);
      }
      idx++;
    }
  },
};
</script>

<style lang="scss">
@import "./forecast.scss";
</style>