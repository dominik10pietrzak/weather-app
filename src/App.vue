<template>
  <div id="app">
    <Nav :fetchWeather="fetchWeather" />
    <Main :weather="weather" />
  </div>
</template>

<script>
import Main from "./components/main/Main.vue";
import Nav from "./components/nav/Nav.vue";

export default {
  name: "App",

  data() {
    return {
      APIKey: "e7eec20a0655f51584d3e1a50afa74ca",
      value: "Warszawa",
      weather: "",
    };
  },
  components: {
    Main,
    Nav,
  },
  methods: {
    async fetchWeather(value) {
      const API = `http://api.openweathermap.org/data/2.5/forecast?q=${value}&appid=${this.APIKey}&units=metric`;

      await fetch(API)
        .then((response) => {
          if (response.ok) {
            return response;
          }
          throw Error("Nie udało się wczytać danych");
        })
        .then((response) => response.json())
        .then((data) => {
          let index = 0;
          for (let i = 0; i < data.list.length; i++) {
            const hour = new Date(data.list[i].dt_txt).getHours();
            if (hour === 15) {
              break;
            } else {
              index++;
            }
          }

          return (this.weather = {
            currentTemp: data.list[0].main.temp,
            city: data.city.name,
            humidity: data.list[0].main.humidity,
            windSpeed: data.list[0].wind.speed,
            description: data.list[0].weather[0].main,
            tempIn1D: data.list[index].main.temp,
            tempIn2D: data.list[index + 8].main.temp,
            tempIn3D: data.list[index + 16].main.temp,
            tempIn4D: data.list[index + 24].main.temp,
            tempIn5D: data.list[index + 32].main.temp,
            descIn1D: data.list[index].weather[0].main,
            descIn2D: data.list[index + 8].weather[0].main,
            descIn3D: data.list[index + 16].weather[0].main,
            descIn4D: data.list[index + 24].weather[0].main,
            descIn5D: data.list[index + 32].weather[0].main,
          });
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  mounted() {
    this.fetchWeather(this.value);
  },
};
</script>

<style lang="scss">
@import "./app.scss";
</style>
