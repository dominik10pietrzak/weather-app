<template>
  <div class="nav">
    <h1>BWeather</h1>
    <div class="date">
      <span>{{ date.dayOfWeek }},</span>
      <span>{{ date.dayOfMonth + date.end + " " + date.month }}</span>
    </div>
    <form @change="isEmpty" @submit.prevent="() => {fetchWeather(value); emptyBar();}">
      <input
        id="search-bar"
        class="search-input"
        type="text"
        placeholder="Search for a city"
        v-model="value"
      />
      <button type="reset" class="delete-button button-hidden">
        <i class="fas fa-times"></i>
      </button>
      <button type="submit" class="search-button">
        <i class="fas fa-search"></i>
      </button>
    </form>
  </div>
</template>

<script>
const date = new Date();

export default {
  name: "Nav",
  props: ["fetchWeather"],
  data() {
    return {
      date: this.displayDate(date),
      value: "",
    };
  },
  methods: {
    emptyBar: () => {
      document.getElementById("search-bar").value = "";
      document.querySelector(".delete-button").classList.add("button-hidden");
    },
    isEmpty() {
      const btn = document.querySelector(".delete-button");
      if (document.getElementById("search-bar").value == "") {
        btn.classList.add("button-hidden");
      } else {
        btn.classList.remove("button-hidden");
      }
    },
    displayDate: () => {
      let dayOfWeek = date.getDay();
      let dayOfMonth = date.getDate();
      let end = "";
      let month = date.getMonth();

      const days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];

      if (dayOfMonth === 1) {
        end = "st";
      } else if (dayOfMonth === 2) {
        end = "nd";
      } else if (dayOfMonth === 3) {
        end = "rd";
      } else {
        end = "th";
      }

      const months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];

      let currentDate = {
        dayOfWeek: days[dayOfWeek],
        dayOfMonth: dayOfMonth,
        end: end,
        month: months[month - 1],
      };

      return currentDate;
    },
  },
  watch: {
    value() {
      this.$emit("change", this.isEmpty());
    },
  },
};
</script>

<style lang="scss">
@import "./nav.scss";
</style>
