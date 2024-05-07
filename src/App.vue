<template>
  <div class="weather" :class="weatherClass">
    <div class="container">

      <div class="card weather-form">
        <input type="text" class="weather-form__input" v-model="searchQuery" @keyup.enter="weatherSearch" placeholder="Enter city">
        <button class="weather-form__btn" @click="weatherSearch">Search</button>
      </div>

      <div class="card weather-load" v-if="loading">Loading...</div>

      <div class="card" v-if="error">{{ erroMessage}}</div>

      <div class="weather-info" v-show="!error && location && temperature !== 0 && description && description">
        <div class="weather-info__text">
          <p class="card">{{ location }}</p>
          <p class="card">{{ temperature }} &deg;C</p>
          <p class="card">{{ description }}</p>
        </div>
      </div>

    </div>

    <div class="weather-bg">
      <div>
        <img class="weather-bg__img bg" src="./assets/images/bg.webp" alt="weather">
        <img class="weather-bg__img sunny" src="./assets/images/sunny.webp" alt="weather Sunny">
        <img class="weather-bg__img partly-cloudy" src="./assets/images/partly-cloudy.webp" alt="weather Partly cloudy">
        <img class="weather-bg__img cloudy" src="./assets/images/cloudy.webp" alt="weather Cloudy">
        <img class="weather-bg__img overcast" src="./assets/images/overcast.webp" alt="weather Overcast">
        <img class="weather-bg__img mist" src="./assets/images/mist.webp" alt="weather Mist">
        <img class="weather-bg__img patchy-rain-possible" src="./assets/images/patchy-rain-possible.webp" alt="weather Patchy rain possible">
        <img class="weather-bg__img patchy-snow-possible" src="./assets/images/patchy-snow-possible.webp" alt="weather Patchy snow possible">
        <img class="weather-bg__img patchy-sleet-possible" src="./assets/images/patchy-sleet-possible.webp" alt="weather Patchy sleet possible">
        <img class="weather-bg__img patchy-freezing-drizzle-possible" src="./assets/images/patchy-freezing-drizzle-possible.webp" alt="weather Patchy freezing drizzle possible">
        <img class="weather-bg__img thundery-outbreaks-possible" src="./assets/images/thundery-outbreaks-possible.webp" alt="weather Thundery outbreaks possible">
        <img class="weather-bg__img blowing-snow" src="./assets/images/blowing-snow.webp" alt="weather Blowing snow">
        <img class="weather-bg__img blizzard" src="./assets/images/blizzard.webp" alt="weather Blizzard">
        <img class="weather-bg__img fog" src="./assets/images/fog.webp" alt="weather Fog">
        <img class="weather-bg__img freezing-fog" src="./assets/images/freezing-fog.webp" alt="weather Freezing fog">
        <img class="weather-bg__img patchy-light-drizzle" src="./assets/images/patchy-light-drizzle.webp" alt="weather Patchy light drizzle">
        <img class="weather-bg__img light-drizzle" src="./assets/images/light-drizzle.webp" alt="weather Light drizzle">
        <img class="weather-bg__img freezing-drizzle" src="./assets/images/freezing-drizzle.webp" alt="weather Freezing drizzle">
        <img class="weather-bg__img heavy-freezing-drizzle" src="./assets/images/heavy-freezing-drizzle.webp" alt="weather Heavy freezing drizzle">
        <img class="weather-bg__img patchy-light-rain" src="./assets/images/patchy-light-rain.webp" alt="weather Patchy light rain">
        <img class="weather-bg__img light-rain" src="./assets/images/light-rain.webp" alt="weather Light rain">
        <img class="weather-bg__img moderate-rain-at-times" src="./assets/images/moderate-rain-at-times.webp" alt="weather Moderate rain at times">
        <img class="weather-bg__img moderate-rain" src="./assets/images/moderate-rain.webp" alt="weather Moderate rain">
        <img class="weather-bg__img heavy-rain-at-times" src="./assets/images/heavy-rain-at-times.webp" alt="weather Heavy rain at times">
        <img class="weather-bg__img heavy-rain" src="./assets/images/heavy-rain.webp" alt="weather Heavy rain">
        <img class="weather-bg__img light-freezing-rain" src="./assets/images/light-freezing-rain.webp" alt="weather Light freezing rain">
        <img class="weather-bg__img moderate-or-heavy-freezing-rain" src="./assets/images/moderate-or-heavy-freezing-rain.webp" alt="weather Moderate or heavy freezing rain">
        <img class="weather-bg__img light-sleet" src="./assets/images/light-sleet.webp" alt="weather Light sleet">
        <img class="weather-bg__img moderate-or-heavy-sleet" src="./assets/images/moderate-or-heavy-sleet.webp" alt="weather Moderate or heavy sleet">
        <img class="weather-bg__img patchy-light-snow" src="./assets/images/patchy-light-snow.webp" alt="weather Patchy light snow">
        <img class="weather-bg__img light-snow" src="./assets/images/light-snow.webp" alt="weather Light snow">
        <img class="weather-bg__img patchy-moderate-snow" src="./assets/images/patchy-moderate-snow.webp" alt="weather Patchy moderate snow">
        <img class="weather-bg__img moderate-snow" src="./assets/images/moderate-snow.webp" alt="weather Moderate snow">
        <img class="weather-bg__img patchy-heavy-snow" src="./assets/images/patchy-heavy-snow.webp" alt="weather Patchy heavy snow">
        <img class="weather-bg__img heavy-snow" src="./assets/images/heavy-snow.webp" alt="weather Heavy snow">
        <img class="weather-bg__img ice-pellets" src="./assets/images/ice-pellets.webp" alt="weather Ice pellets">
        <img class="weather-bg__img light-rain-shower" src="./assets/images/light-rain-shower.webp" alt="weather Light rain shower">
        <img class="weather-bg__img moderate-or-heavy-rain-shower" src="./assets/images/moderate-or-heavy-rain-shower.webp" alt="weather Moderate or heavy rain shower">
        <img class="weather-bg__img torrential-rain-shower" src="./assets/images/torrential-rain-shower.webp" alt="weather Torrential rain shower">
        <img class="weather-bg__img light-sleet-showers" src="./assets/images/light-sleet-showers.webp" alt="weather Light sleet showers">
        <img class="weather-bg__img moderate-or-heavy-sleet-showers" src="./assets/images/moderate-or-heavy-sleet-showers.webp" alt="weather Moderate or heavy sleet showers">
        <img class="weather-bg__img light-snow-showers" src="./assets/images/light-snow-showers.webp" alt="weather Light snow showers">
        <img class="weather-bg__img moderate-or-heavy-snow-showers" src="./assets/images/moderate-or-heavy-snow-showers.webp" alt="weather Moderate or heavy snow showers">
        <img class="weather-bg__img light-showers-of-ice-pellets" src="./assets/images/light-showers-of-ice-pellets.webp" alt="weather Light showers of ice pellets">
        <img class="weather-bg__img moderate-or-heavy-showers-of-ice-pellets" src="./assets/images/moderate-or-heavy-showers-of-ice-pellets.webp" alt="weather Moderate or heavy showers of ice pellets">
        <img class="weather-bg__img patchy-light-rain-with-thunder" src="./assets/images/patchy-light-rain-with-thunder.webp" alt="weather Patchy light rain with thunder">
        <img class="weather-bg__img moderate-or-heavy-rain-with-thunder" src="./assets/images/moderate-or-heavy-rain-with-thunder.webp" alt="weather Moderate or heavy rain with thunder">
        <img class="weather-bg__img patchy-light-snow-with-thunder" src="./assets/images/patchy-light-snow-with-thunder.webp" alt="weather Patchy light snow with thunder">
        <img class="weather-bg__img moderate-or-heavy-snow-with-thunder" src="./assets/images/moderate-or-heavy-snow-with-thunder.webp" alt="weather Moderate or heavy snow with thunder">
        <img class="weather-bg__img clear" src="./assets/images/clear.webp" alt="weather Clear">

      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      location: '',
      temperature: 0,
      description: '',
      loading: false,
      error: false,
      searchQuery: '',
      erroMessage: 'Doesn\'t correct city or cityname isn\'t in database. Please, try again'

    }
  },
computed: {
  weatherClass() {
    const weatherConditions = [
      { condition: 'Sunny', className: 'sunny' },
      { condition: 'Partly cloudy', className: 'partly-cloudy' },
      { condition: 'Cloudy', className: 'cloudy' },
      { condition: 'Overcast', className: 'overcast' },
      { condition: 'Mist', className: 'mist' },
      { condition: 'Patchy rain possible', className: 'patchy-rain' },
      { condition: 'Patchy snow possible', className: 'patchy-snow' },
      { condition: 'Patchy sleet possible', className: 'patchy-sleet' },
      { condition: 'Patchy freezing drizzle possible', className: 'patchy-freezing-drizzle' },
      { condition: 'Thundery outbreaks possible', className: 'thundery-outbreaks' },
      { condition: 'Blowing snow', className: 'blowing-snow' },
      { condition: 'Blizzard', className: 'blizzard' },
      { condition: 'Fog', className: 'fog' },
      { condition: 'Freezing fog', className: 'freezing-fog' },
      { condition: 'Patchy light drizzle', className: 'patchy-light-drizzle' },
      { condition: 'Light drizzle', className: 'light-drizzle' },
      { condition: 'Freezing drizzle', className: 'freezing-drizzle' },
      { condition: 'Heavy freezing drizzle', className: 'heavy-freezing-drizzle' },
      { condition: 'Patchy light rain', className: 'patchy-light-rain' },
      { condition: 'Light rain', className: 'light-rain' },
      { condition: 'Moderate rain at times', className: 'moderate-rain-at-times' },
      { condition: 'Moderate rain', className: 'moderate-rain' },
      { condition: 'Heavy rain at times', className: 'heavy-rain-at-times' },
      { condition: 'Heavy rain', className: 'heavy-rain' },
      { condition: 'Light freezing rain', className: 'light-freezing-rain' },
      { condition: 'Moderate or heavy freezing rain', className: 'moderate-heavy-freezing-rain' },
      { condition: 'Light sleet', className: 'light-sleet' },
      { condition: 'Moderate or heavy sleet', className: 'moderate-heavy-sleet' },
      { condition: 'Patchy light snow', className: 'patchy-light-snow' },
      { condition: 'Light snow', className: 'light-snow' },
      { condition: 'Patchy moderate snow', className: 'patchy-moderate-snow' },
      { condition: 'Moderate snow', className: 'moderate-snow' },
      { condition: 'Patchy heavy snow', className: 'patchy-heavy-snow' },
      { condition: 'Heavy snow', className: 'heavy-snow' },
      { condition: 'Ice pellets', className: 'ice-pellets' },
      { condition: 'Light rain shower', className: 'light-rain-shower' },
      { condition: 'Moderate or heavy rain shower', className: 'moderate-heavy-rain-shower' },
      { condition: 'Torrential rain shower', className: 'torrential-rain-shower' },
      { condition: 'Light sleet showers', className: 'light-sleet-showers' },
      { condition: 'Moderate or heavy sleet showers', className: 'moderate-heavy-sleet-showers' },
      { condition: 'Light snow showers', className: 'light-snow-showers' },
      { condition: 'Moderate or heavy snow showers', className: 'moderate-heavy-snow-showers' },
      { condition: 'Light showers of ice pellets', className: 'light-showers-of-ice-pellets' },
      { condition: 'Moderate or heavy showers of ice pellets', className: 'moderate-heavy-showers-of-ice-pellets' },
      { condition: 'Patchy light rain with thunder', className: 'patchy-light-rain-with-thunder' },
      { condition: 'Moderate or heavy rain with thunder', className: 'moderate-heavy-rain-with-thunder' },
      { condition: 'Patchy light snow with thunder', className: 'patchy-light-snow-with-thunder' },
      { condition: 'Moderate or heavy snow with thunder', className: 'moderate-heavy-snow-with-thunder' },
      { condition: 'Clear', className: 'clear' },
    ];

    for (const { condition, className } of weatherConditions) {
      if (this.description.includes(condition)) {
        return className
      }
    }

    return 'weather'
  }
}
,
methods: {
    weatherSearch() {
      this.loading = true
      this.error = false
      fetch(`http://api.weatherapi.com/v1/current.json?key=c66fe224c6dd40ac96d173530243004&q=${this.searchQuery}`)
        .then(response => response.json())
        .then(data => {
          this.loading = false
          this.location = data.location.name
          this.temperature = data.current.temp_c
          this.description = data.current.condition.text
          this.resetSearchQuery();
        })
        .catch(error => {
          this.loading = false
          this.error = true
          console.error(error);
        })
    },
    resetSearchQuery() {
      this.searchQuery = ''
    }
  }
}
</script>