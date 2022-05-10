<script>
export default {
  data() {
    return {
      realTemp: 0,
      feelsLike: 0,
      humidity: 0,
      windSpeed: 0,
      weather: '',
      airPressure: 0,
    }
  },
  async mounted() {

    //Async-Await Based Way
    // MUST be on SHGuest network.
    const response = await fetch("http://172.17.103.69:8080")
    const data = await response.json()
    // Create loading bar / API Down indicator
    this.realTemp = data.realTemp.toFixed()
    this.feelsLike = data.feelsLike.toFixed()
    this.windSpeed = data.windSpeed.toFixed()
    this.humidity = data.humidity.toFixed()
    this.weather = data.sky
    this.airPressure = (data.airPressure).toFixed(2)

    console.log(data)
  }

}
</script>

<template>
  <div class="jumbotronWeather">
    <h1>South Hills, Altoona</h1>
    <div class="row marketing">
      <div class="col-lg-6">
        <h4>Temp</h4>
        <p>{{ realTemp }}&deg;F</p>
      </div>

      <div class="col-lg-6">
        <h4>Feels Like</h4>
        <p>{{ feelsLike }}&deg;F</p>
      </div>
    </div>

    <div class="row marketing">
      <div class="col-lg-6">
        <h4>Weather</h4>
        <p>{{ weather }}</p>
      </div>

      <div class="col-lg-6">
        <h4>Humidity</h4>
        <p>{{ humidity }}%</p>
      </div>
    </div>

    <div class="row marketing">
      <div class="col-lg-6">
        <h4>Wind Speed</h4>
        <p>{{ windSpeed }}mph</p>
      </div>

      <div class="col-lg-6">
        <h4>Air Pressure</h4>
        <p>{{ airPressure }}PSI</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
</style>