<script>
export default {
    data() {
        return {
            realTemp: 0,
            feelsLike: 0,
            humidity: 0,
            windSpeed: 0,
        }
    },
    async mounted() {

        //Async-Await Based Way
        const response = await fetch("http://172.17.103.69:8080/")
        const data = await response.json()
        this.realTemp = data.realTemp
        this.feelsLike = data.feelsLike
        this.windSpeed = data.windSpeed
        this.humidity = data.humidity

        console.log(data)
    }
    
}
</script>

<template>
    <div class="jumbotron">
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
          <h4>Humidity</h4>
          <p>{{ humidity }}%</p>
        </div>

        <div class="col-lg-6">
          <h4>Wind Speed</h4>
          <p>{{ windSpeed }}mph</p>
        </div>
      </div>
    </div>
</template>

<style scoped>

</style>