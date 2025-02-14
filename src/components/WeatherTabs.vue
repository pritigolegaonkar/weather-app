<template>
    <div>
      <button
        v-for="city in cities"
        :key="city"
        @click="changeCity(city)"
        :class="selectedCity === city ? 'border-b-4 border-red-500 font-bold' : 'text-gray-600'"
      >
        {{ city.toUpperCase() }}
      </button>
    </div>

    <WeatherCard :city="selectedCity" :weather="weather" :forecast="forecast" :lastUpdated="lastUpdated" />
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import WeatherCard from "./WeatherCard.vue";
import { getWeather, getForecast } from "../services/weatherService";
import type { WeatherData, ForecastData } from "../types/weather";

const cities = ["Rio de Janeiro", "Beijing", "Los Angeles"];
const selectedCity = ref<string>(cities[2]); // Default: Los Angeles

const weather = ref<WeatherData | null>(null);
const forecast = ref<ForecastData | null>(null);
const lastUpdated = ref<string>("");

// Fetch weather data
const fetchWeather = async () => {
  weather.value = await getWeather(selectedCity.value);
  forecast.value = await getForecast(selectedCity.value);
  lastUpdated.value = new Date().toLocaleString();
};

// Update weather when a tab is clicked
const changeCity = async (city: string) => {
  selectedCity.value = city;
  await fetchWeather();
};

// Fetch weather on mount
onMounted(fetchWeather);
</script>