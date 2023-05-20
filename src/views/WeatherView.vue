<template>
  <div>
    <div class="flex justify-center space-x-4 items-center">
      <select class="border-solid border-2 rounded p-2" v-model="selected">
        <option disabled value="">Please select one</option>
        <option>Miami</option>
        <option>New York</option>
        <option>Los Angeles</option>
      </select>
      <div>Or</div>
      <div
        class="p-2 cursor-pointer bg-transparent text-sm text-gray-600 font-semibold border rounded border-gray-500 hover:bg-gray-500 hover:text-white active:bg-gray-700 active:text-white active:border-transparent"
        @click="handleAutoLocationDetection"
      >
        Auto detect your location
      </div>
    </div>
    <Loading v-if="isLoading" />
    <div v-else class="flex justify-center">
      <div class="flex-col">
        <div class="flex justify-center text-indigo-500 mt-4 mb-2 text-2xl">
          {{ rawData && rawData.name ? rawData.name : selected }}
        </div>
        <div class="flex justify-center text-4xl">
          {{ rawData.main && rawData.main.temp ? rawData.main.temp : 'Null' }}&degF
        </div>
        <div class="flex justify-center items-center">
          <div><img id="wicon" :src="iconSource" alt="Weather icon" /></div>
          <div>{{ locationWeatherData.main ? locationWeatherData.main : 'Null' }}</div>
        </div>
        <div class="flex justify-center">
          L {{ rawData.main && rawData.main.temp_min ? rawData.main.temp_min : 'Null' }}&degF - H
          {{ rawData.main && rawData.main.temp_max ? rawData.main.temp_max : 'Null' }}&degF
        </div>
        <div class="flex justify-start">Description: {{ locationWeatherData.description }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Loading from '../components/Loading.vue'
import DetectLocationBrowserMixin from '../components/Mixins/DetectLocationBrowser.vue'

export default {
  components: {
    Loading
  },
  mixins: [DetectLocationBrowserMixin],
  data() {
    return {
      isLoading: true,
      selected: 'Miami',
      locationDetection: {},
      rawData: {},
      locationWeatherData: {},
      apiKey: null
    }
  },
  created() {
    if (process.env.NODE_ENV !== 'production') {
      this.apiKey = 'f7a16a6059d51eb4e3e136c827378c17'
    }
    this.fetchWeatherInfoWithCityName()
  },
  watch: {
    locationDetection() {
      this.fetchWeatherInfoWithCords()
    },
    selected() {
      this.fetchWeatherInfoWithCityName()
    }
  },
  computed: {
    iconSource() {
      if (Object.keys(this.rawData).length > 0 && this.locationWeatherData.icon) {
        return `http://openweathermap.org/img/w/${this.locationWeatherData.icon}.png`
      }
      return ''
    }
  },
  methods: {
    fetchWeatherInfoWithCityName() {
      this.isLoading = true
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.selected}&units=imperial&appid=${this.apiKey}`
        )
        .then((response) => {
          this.rawData = response.data
          this.locationWeatherData = this.rawData.weather[0]
          this.isLoading = false
        })
        .catch((error) => {
          console.log(error.message)
        })
    },

    fetchWeatherInfoWithCords() {
      this.isLoading = true
      axios
        .get(
          `https://api.openweathermap.org/data/2.5/weather?lat=${this.locationDetection.lat}&lon=${this.locationDetection.long}&units=imperial&appid=${this.apiKey}`
        )
        .then((response) => {
          this.rawData = response.data
          this.locationWeatherData = this.rawData.weather[0]
          this.isLoading = false
        })
        .catch((error) => {
          console.log(error.message)
        })
    }
  }
}
</script>
