<template>
  <div>
    <NextHours :forecast="forecast" />
    <NextFiveDays :forecast="forecast" />

    <div class="mt-4">
      Last updated on {{ lastUpdated }}
    </div>
  </div>
</template>

<script setup lang="ts">
import { WeatherData, ForecastData } from "../types/weather";
import NextFiveDays from "./NextFiveDays.vue";
import NextHours from "./NextHours.vue";

defineProps<{
  city: string;
  weather: WeatherData | null;
  forecast: ForecastData | null;
  lastUpdated: string;
}>();
</script>