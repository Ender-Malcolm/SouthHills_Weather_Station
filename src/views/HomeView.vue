<script setup>
import currentWeatherContainer from "../components/icons/currentWeatherContainer.vue";



  components: { currentWeatherContainer }</script>

<template>
  <div class="container">
    <div class="header clearfix">
      <nav>
        <ul class="nav nav-pills pull-right">
          <li role="presentation" class="active">
            <a href="#">Bridge</a>
          </li>
        </ul>
      </nav>
      <h3 class="text-muted">South Hills Weather Readings</h3>
    </div>

    <current-weather-container />

    <div class="row marketing">
      <div class="card">
        <h4>Subheading</h4>
        <img src="/southhillsBackground.jpg" class="card-img-top" />
        <div class="card-body">
          <h5 class="card-title">Card Title</h5>
          <p
            class="card-text"
          >Donec id elit non mi porta gravida at eget metus. Maecenas faucibus mollis interdum.</p>
        </div>
      </div>
    </div>

    <footer class="footer">
      <p>&copy; March, 2022 Ender Malcolm, South Hills</p>
    </footer>
  </div>
  <!-- /container -->
</template>
