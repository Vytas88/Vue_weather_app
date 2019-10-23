<template>
  <div class="container">
    <div class="title">Worldwide Weather App</div>
    <div class="col-lg-4 col-lg-offset-4">
      <div class="input-group mb-3">
        <input
          v-model.lazy="currentCity"
          value
          type="text"
          class="form-control"
          placeholder="Enter a valid city"
          aria-label="Enter a valid city"
          aria-describedby="button-addon2"
        />
        <div class="input-group-append">
          <button
            @click="getWeather"
            class="btn btn-outline-secondary"
            type="button"
            id="button-addon2"
          >Get weather!</button>
        </div>
      </div>
    </div>

    <!-- Forecast values -->
    <div
      class="forecast__values container shadow p-4 mt-4"
      v-if="currentWeather && currentWeather.cod == 200"
    >
      <div class="m-2">
        <FavoriteIcon :active="weather.isFavored" @click="$emit('favorite', weather)" />
        <strong>City:</strong>
        {{ currentWeather.name }}
      </div>
      <div class="m-2">
        <strong>Weather condition:</strong>
        <span class="text-capitalize">{{ currentWeather.weather[0].description }}</span>
      </div>
      <div class="m-2">
        <strong>Temperature:</strong>
        {{ currentWeather.main.temp }}° C
        <span>
          <img :src="this.currentIcon" alt="Weather Condition Representation Icon" />
        </span>
      </div>
      <div class="m-2">
        <strong>Wind Speed:</strong>
        {{ currentWeather.wind.speed }} m/s
      </div>
    </div>
    <div v-else>"{{ currentCity }}" is not a valid.</div>
  </div>
</template>

<script>
import axios from "axios";
import FavoriteIcon from "@/components/FavoriteIcon";

export default {
  components: {
    FavoriteIcon
  },
  name: "Forecast",
  props: {
    weather: {
      type: Object,
      required: true,
      default: () => ({
        currentWeather: null,
        currentCity: "Vilnius",
        currentCountry: "world",
        unit: "metric",
        currentIcon: null
      })
    }
  },
  data() {
    return {
      currentWeather: null,
      currentCity: "Vilnius",
      currentCountry: "world",
      unit: "metric",
      currentIcon: null
    };
  },
  methods: {
    getWeather() {
      // make axios request to open weather api
      axios
        .get(
          "https://api.openweathermap.org/data/2.5/weather?q=" +
            this.currentCity +
            "," +
            this.currentCountry +
            "&appid=80b1c2c93c46dd5e049912b4df043b52&units=" +
            this.unit +
            ""
        )
        .then(response => {
          // takes response object & stores it in currentWeather
          this.currentWeather = response.data;
          // takes value for image icon
          this.currentIcon =
            "https://openweathermap.org/img/w/" +
            this.currentWeather.weather[0].icon +
            ".png";
        })
        .catch(function(error) {
          // handle error
          console.log(error);
        });
    }
  },
  mounted() {
    // Calls Weather API response onload
    this.getWeather();
  }
};
</script>
<style scoped lang="scss">
.title {
  padding-top: 30px;
  color: black;
}
.container {
  background-image: url("~@/assets/weather.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
}
.title {
  font-size: 30px;
}
.forecast__values {
  color: black;
}
.forecast__values--favorite {
  display: flex;
  justify-content: center;
}
.input-group {
  width: 400px;
  margin: 0 auto;
}
.col-lg-4 {
  width: 100%;
  padding-left: 250px;
  padding-top: 30px;
}
.btn {
  background-color: unset;
  color: black;
}
</style>
