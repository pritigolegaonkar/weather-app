<template>
  <div class="weather-card-container">
    <h2 style="text-align: left;">Next hours</h2>
    <div v-if="forecast" class="grid-col-container">
      <div 
        v-for="hour in nextFiveHours" 
        :key="hour.dt_txt" 
        class="flex flex-col items-center min-w-[80px] text-gray-800">
          <div><span class="text-lg font-bold">{{ Math.round(hour.main.temp) }}°</span></div>
          <span class="text-blue-600 text-sm">{{ hour.pop ? hour.pop * 100 : 0 }}%</span>
          <img :src="getIconUrl(hour.weather[0].icon)"  alt="Weather Icon" class="w-6 h-6"/>
          <span class="text-sm">{{ formatTime(hour.dt_txt) }}</span>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, defineProps } from "vue";
import type { ForecastData } from "../types/weather";

const props = defineProps<{ forecast: ForecastData | null }>();

const nextFiveHours = computed(() => props.forecast?.list.slice(0, 5) || []);

const formatTime = (dateTime: string): string => {
  return new Date(dateTime).toLocaleTimeString([], { hour: "numeric", minute: "2-digit" });
};

const getIconUrl = (icon: string) => `https://openweathermap.org/img/wn/${icon}.png`;
</script>