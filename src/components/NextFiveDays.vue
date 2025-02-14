<template>
  <div class="weather-card-container">
    <h2  style="text-align: left;">Next 5 days</h2>
      <div v-if="forecast" class="grid-row-container">
        <div 
          v-for="(day, index) in nextDays" 
          :key="index" 
          class="grid-row-col-container">

          <img :src="getIconUrl(day.weather[0].icon)"  alt="Weather Icon" class="w-6 h-6"/>

          <span>
            <div>
            <span class="font-bold">{{ formatDate(day.dt_txt) }}</span></div>
            <div>
            <span class="text-sm">{{ day.weather[0].description }}</span></div>
          </span>
          <span class="font-bold">{{ Math.round(day.main.temp_max) }}°</span>
          <span class="font-bold">{{ Math.round(day.main.temp_min) }}°</span>  
        </div>
      </div>
    </div>


</template>

<script setup lang="ts">
import { computed, defineProps } from "vue";
import type { ForecastData } from "../types/weather";

const props = defineProps<{ forecast: ForecastData | null }>();

const nextDays = computed(() => {
  if (!props.forecast) return [];
  return props.forecast.list.filter((entry) => entry.dt_txt.includes("12:00:00")).slice(0, 5);
});

const formatDate = (dateTime: string): string => {
  return new Date(dateTime).toLocaleDateString([], { weekday: "short", month: "short", day: "numeric" });
};

const getIconUrl = (icon: string) => `https://openweathermap.org/img/wn/${icon}.png`;
</script>