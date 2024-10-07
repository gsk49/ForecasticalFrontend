<template>
  <div class="weather-app">
    <header>
      <h1>Forecastical</h1>
      <router-link to="/profile">Go to Profile</router-link>
    </header>
    <div class="content">
      <div class="left-column">
        <div class="current-weather">
          <p>Current Location: {{ currentLocation }}</p>
          <p>{{ temperature }} degrees; {{ condition }}</p>
          <span class="weather-icon">☁️</span>
        </div>
        <div class="today-forecast">
          <h2>Today's Forecast</h2>
          <div></div>
          <!-- Add today's forecast details here -->
        </div>
        <div class="weekly-forecast">
          <h2>Weekly Forecast</h2>
          <!-- Add weekly forecast details here -->
          <div class="forecast-grid">
            <div
              v-for="dayForecast in weeklyConditions"
              :key="dayForecast.day"
              class="day"
            >
              <h4>{{ dayForecast.day }}</h4>
              <img
                :src="getWeatherIcon(dayForecast.condition)"
                alt="weather icon"
                class="weather-icon"
              />
              <p>
                {{ dayForecast.condition }}<br />
                {{ dayForecast.temperature }}&deg;
              </p>
            </div>
          </div>
        </div>
        <div class="update-location">
          <button @click="updateLocation">
            <span class="icon">↻</span>
            Update Location
          </button>
        </div>
      </div>
      <div class="right-column">
        <div class="supplementary-conditions">
          <h2>Supplementary Conditions</h2>
          <p>Air: {{ air }}</p>
          <p>UV Index: {{ uvIndex }}</p>
          <p>Humidity: {{ humidity }}</p>
          <p>Pressure: {{ pressure }}</p>
        </div>
        <div class="updated-user-forecast">
          <h2>Updated User Forecast</h2>
          <!-- Add user forecast map or details here -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "WeatherApp",
  data() {
    return {
      currentLocation: "Cleveland, OH",
      temperature: 42,
      condition: "Partly cloudy",
      air: "23",
      uvIndex: "9",
      humidity: "78%",
      pressure: "1,014 hPa",
      weatherIcons: {
        sunny: require("../assets/sunny.png"),
        rainy: require("../assets/rainy.png"),
        partly_cloudy: require("../assets/partly_cloudy.png"),
      },
      weeklyConditions: [
        { day: "Sunday", condition: "sunny", temperature: "79" },
        { day: "Monday", condition: "partly cloudy", temperature: "73" },
        { day: "Tuesday", condition: "rainy", temperature: "60" },
        { day: "Wednesday", condition: "partly cloudy", temperature: "67" },
        { day: "Thursday", condition: "sunny", temperature: "75" },
        { day: "Friday", condition: "partly cloudy", temperature: "73" },
        { day: "Saturday", condition: "rainy", temperature: "71" },
      ],
    };
  },
  methods: {
    updateLocation() {
      // Implement location update logic here
      console.log("Updating location...");
    },
    getWeatherIcon(condition) {
      // Map the condition to an icon name
      const conditionMapping = {
        "partly cloudy": "partly_cloudy",
        cloudy: "cloudy",
        sunny: "sunny",
        rainy: "rainy",
      };
      const mappedCondition =
        conditionMapping[condition.toLowerCase()] || "default";
      return this.weatherIcons[mappedCondition];
    },
  },
  computed: {
    weatherIcon() {
      // Map condition to the corresponding icon
      const conditionMapping = {
        "Partly cloudy": "partly_cloudy", // Map condition with space to the key with an underscore
        cloudy: "partly_cloudy",
        sunny: "Sunny",
        rainy: "Rainy",
      };

      const mappedCondition =
        conditionMapping[this.condition] || this.condition;
      return (
        this.weatherIcons[mappedCondition] ||
        require("../assets/partly_cloudy.png")
      );
    },
  },
};
</script>

<style scoped>
.weather-app {
  font-family: Arial, sans-serif;
  color: white;
  background-color: #1e1e1e;
  padding: 20px;
  border-radius: 10px;
}

header {
  background-color: #2c3e50;
  padding: 10px;
  text-align: center;
  border-radius: 5px;
}

.content {
  display: flex;
  margin-top: 20px;
}

.left-column {
  flex: 3;
  margin-right: 20px;
}

.right-column {
  flex: 1;
}

.update-location,
.current-weather,
.today-forecast,
.weekly-forecast,
.supplementary-conditions,
.updated-user-forecast {
  background-color: #34495e;
  padding: 15px;
  margin-bottom: 20px;
  border-radius: 5px;
}

.update-location button {
  background-color: #3498db;
  border: none;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
}

.weather-icon {
  font-size: 2em;
}

h2 {
  margin-top: 0;
}

.weekly-forecast .forecast-grid {
  display: flex;
  justify-content: center; /* Centers the divs horizontally */
  gap: 10px; /* Adjusts spacing between divs */
  flex-wrap: wrap; /* Allows wrapping if screen size is too small */
}

.weekly-forecast .day {
  flex: 1 1 calc(100% / 7); /* Distributes each div equally */
  max-width: 100px; /* Optional: Maximum width for each div */
  text-align: center;
}

.weekly-forecast img {
  width: 50px;
  height: 50px;
}
</style>
