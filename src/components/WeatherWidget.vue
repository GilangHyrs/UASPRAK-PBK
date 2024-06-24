<template>
  <div class="weather-widget">
    <h2>Weather Widget</h2>
    <div class="search-bar">
      <input v-model="city" placeholder="Enter city name" @keyup.enter="getWeather" />
      <button @click="getWeather">Search</button>
    </div>
    <div v-if="weather" class="weather-info">
      <div class="weather-item animate-item">
        <p class="bold-text"><strong>Location:</strong> {{ weather.name }}</p>
        <img src="../assets/loc.png" alt="location icon" />
        <div class="weather-border"></div>
      </div>
      <div class="weather-item animate-item">
        <p class="bold-text"><strong>Temperature:</strong> {{ weather.main.temp }}°C</p>
        <img src="../assets/temp.png" alt="temperature icon" />
        <div class="weather-border"></div>
      </div>
      <div class="weather-item animate-item">
        <p class="bold-text"><strong>Weather:</strong> {{ weather.weather[0].description }} </p>
        <img :src="`http://openweathermap.org/img/wn/${weather.weather[0].icon}.png`" alt="weather icon" />
        <div class="weather-border"></div>
      </div>
    </div>
    <div v-else>
      <p>Enter a city name to see the weather.</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const city = ref('')
const weather = ref(null)

const getWeather = async () => {
  const apiKey = 'ceb97d9ca273e7696ff7f99b1a1fa728'
  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city.value}&units=metric&appid=${apiKey}`

  try {
    const response = await axios.get(url)
    weather.value = response.data
  } catch (error) {
    console.error(error)
    weather.value = null
  }
}
</script>

<style scoped>
.weather-widget {
  padding: 20px;
  border: 1px solid var(--medium-red);
  border-radius: 10px;
  max-width: 700px;
  margin: 100px auto 50px auto; 
  text-align: center;
  background-color: var(--light-beige);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.weather-widget h2 {
  color: var(--dark-red);
  font-size: 36px;
  font-weight: bold;
  margin-bottom: 20px;
}

.search-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.search-bar input {
  padding: 10px;
  width: 70%;
  margin-right: 10px;
  border: 1px solid var(--medium-red);
  border-radius: 5px;
  background-color: var(--beige);
}

.search-bar button {
  padding: 10px;
  border: 1px solid var(--dark-red);
  background-color: var(--medium-red);
  color: var(--light-beige);
  cursor: pointer;
  border-radius: 5px;
}

.search-bar button:hover {
  background-color: var(--dark-red);
}

.weather-info {
  margin-top: 40px; 
  display: flex;
  justify-content: center; 
  align-items: center;
  flex-wrap: wrap; 
}

.weather-item {
  margin: 20px; 
  border: 1px solid var(--medium-red);
  border-radius: 5px;
  padding: 20px;
  background-color: var(--beige);
  text-align: center;
  width: 220px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  animation: backgroundColorChange 3s ease infinite; 
}

.weather-item img {
  margin-top: 10px;
  width: 35px;
  height: 35px;
}

.weather-item p {
  margin: 0;
  color: var(--dark-red);
  font-weight: bold; 
}

.weather-border {
  border-top: 1px solid var(--medium-red);
  margin-top: 10px;
  padding-top: 10px;
}



.animate-item {
  animation: fadeIn 2s ease-out;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: translateY(-10px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes backgroundColorChange {
  0% {
    background-color: var(--beige);
  }
  50% {
    background-color: var(--light-beige);
  }
  100% {
    background-color: var(--beige);
  }
}
</style>
