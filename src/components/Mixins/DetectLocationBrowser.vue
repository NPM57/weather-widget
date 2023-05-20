<script>
export default {
  data() {
    return {
      locationDetection: {}
    }
  },
  methods: {
    async handleAutoLocationDetection() {
      navigator.geolocation.getCurrentPosition(
        (position) => {
          this.locationDetection = {
            lat: position.coords.latitude,
            long: position.coords.longitude
          }
        },
        (error) => {
          console.log(error.message)
        }
      )
    }
  }
}
</script>
