<template>
    <div class="hour-details">
      <p class="time">{{ displayTime || formatTime(hourWeather.time) }}</p>
      <img :src="getWeatherIcon(hourWeather.condition)" alt="Weather Icon" class="weather-icon" />
      <p class="temperature">{{ hourWeather.temperature }}°</p>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      hourWeather: Object,
      displayTime: String
    },
    methods: {
      formatTime(timestamp) {
        const date = new Date(timestamp * 1000); // Assuming UNIX timestamp in seconds
        return date.toLocaleTimeString([], { hour: "numeric", minute: "2-digit" });
      },
      getWeatherIcon(condition) {
        // Replace this with actual logic for mapping conditions to icons
        const iconMap = {
          sunny: "https://example.com/sunny.png",
          cloudy: "https://example.com/cloudy.png",
          rain: "https://example.com/rain.png"
        };
        return iconMap[condition] || "https://example.com/default.png";
      }
    }
  };
  </script>