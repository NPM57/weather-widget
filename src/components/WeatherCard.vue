<template>
  <div class="mx-auto p-4 flex justify-center">
    <div class="flex flex-wrap">
      <div class="w-full px-2">
        <div
          class="bg-gray-700 text-white relative min-w-0 break-words rounded-lg overflow-hidden shadow-sm mb-4 w-full dark:bg-gray-600"
        >
          <div class="px-6 py-6 relative">
            <div class="flex mb-4 justify-between items-center">
              <div>
                <h5 class="mb-0 font-medium text-xl">{{ cityName }}</h5>
                <h6 class="mb-0">{{ currentDateTime }}</h6>

                <div class="flex items-center">
                  <img id="wicon" :src="weatherIcon" alt="Weather icon" />
                  <small>{{ weatherStatus }}</small>
                </div>
              </div>
              <div class="text-right">
                <h3 class="font-bold text-4xl mb-0">
                  <span>{{ Math.round(currentTemp) }}&deg;</span>
                </h3>
              </div>
            </div>
            <div class="block sm:flex justify-between items-center flex-wrap">
              <div class="w-full sm:w-1/2">
                <div class="flex mb-2 justify-between items-center">
                  <span>Temp</span
                  ><small class="px-2 inline-block">{{ currentTemp }}&nbsp;&deg;</small>
                </div>
              </div>
              <div class="w-full sm:w-1/2">
                <div class="flex mb-2 justify-between items-center">
                  <span>Feels like</span
                  ><small class="px-2 inline-block">{{ feelsLike }}&nbsp;&deg;</small>
                </div>
              </div>
              <div class="w-full sm:w-1/2">
                <div class="flex mb-2 justify-between items-center">
                  <span>Temp min</span
                  ><small class="px-2 inline-block">{{ tempMin }}&nbsp;&deg;</small>
                </div>
              </div>
              <div class="w-full sm:w-1/2">
                <div class="flex mb-2 justify-between items-center">
                  <span>Temp max</span
                  ><small class="px-2 inline-block">{{ tempMax }}&nbsp;&deg;</small>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    cityName: {
      type: String,
      required: true
    },
    currentTemp: {
      type: Number,
      default: null,
      required: false
    },
    feelsLike: {
      type: Number,
      default: null,
      required: false
    },
    tempMax: {
      type: Number,
      default: null,
      required: false
    },
    tempMin: {
      type: Number,
      default: null,
      required: false
    },
    weatherStatus: {
      type: String,
      default: null,
      required: false
    },
    weatherIcon: {
      type: String,
      default: null,
      required: false
    }
  },

  computed: {
    currentDateTime() {
      return new Date().toLocaleString()
    }
  }
}
</script>
