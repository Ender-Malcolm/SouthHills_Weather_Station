<script setup>
import currentWeatherContainer from "../components/currentWeatherContainer.vue";
import navBar from "../components/navBar.vue";
import FOOTER from "../components/footer.vue";



components: { currentWeatherContainer}
</script>

<template>
<head>
  <!--Refresh page automatically every 5 minutes-->
  <meta http-equiv="Refresh" content="60*5">
</head>
  <div class="container">
    <div class="header clearfix">
      <navBar />
      <br>
      <h3 class="text-muted">South Hills Weather Readings</h3>
    </div>
    
    <current-weather-container />

    <!-- <div class="row marketing">
      <div class="card">
        <h4>Subheading</h4>
        <img src="/southhillsBackground.jpg" class="card-img-top" />
        <div class="card-body">
          <h5 class="card-title">Card Title</h5>
          <p class="card-text">Donec id elit non mi porta gravida at eget metus. Maecenas faucibus mollis interdum.</p>
        </div>
      </div>
    </div> -->
    <br>
    <br>
    <br>
    <FOOTER />
  </div>
  <!-- /container -->
</template>
