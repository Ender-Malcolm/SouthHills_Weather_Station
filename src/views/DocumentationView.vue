<script setup>
import currentWeatherContainer from "../components/currentWeatherContainer.vue";
import navBar from "../components/navBar.vue";
import FOOTER from "../components/footer.vue";

components: { currentWeatherContainer }</script>

<template>
  <div class="container">
    <div class="header clearfix">
      <navBar />
      <br>
      <h3 class="text-muted">Weather Station Documentation</h3>
    </div>
    <div class="container" style="text-align: justify; text-justify: auto;">
      <h3>Intro</h3>
      <p>
        Greetings, and welcome to my Weather Station! My name is Nathan Connacher, though I also go by Ender Malcolm, my
        pen name.
        I would like to thank you for visiting this site! I've put a lot of work into this project, and have had a lot
        of fun along the way.
        So let me tell you now a bit about this project, the challenges and breakthroughs, and why I chose to make a
        weather station.
      </p>
      <h4>Why I made a Weather Station</h4>
      <p>
        This project began as an idea to simply provide temperature data for my classroom. That almost instantly fell
        to the idea of making a full weather station. I have had interest in weather for a long time, especially as the
        bad stuff seems to always follow me around. Every time I leave the state of Pennsylvania, there's some freak
        weather event. With that in mind, I decided that being able to track the weather would be a useful item,
        especially with
        my own equipment.
      </p>
      <p>
        Along with my interest in the weather, this project also serves a useful purpose to the local community. The
        school is able to check out real time weather data and report it to students. On top of this, I would like to
        contribute
        the data to the National Weather Service; as a registered weather station it can provide real time data for the
        immediate
        area, an important capability in my opinion. As a bonus, the data can be logged locally, and parted out to
        research
        centers for their use.
      </p>
      <h4>Challenges and Breakthroughs</h4>
      <p>
        There were plenty of challenges with this project; chief among them being "What sensors am I going to use?". I
        needed something that would work with my Raspberry Pi, have the equipment I needed, and also not do everything
        itself.
        I decided I wanted the SparkFun Weather Station Kit, which included an anemometer, a weather vane, and rain
        guage. The sensors are all analogue, and require connections for RJ11 Phone Connectors. This required me to also
        aquire
        special 'breakout boards', which convert the RJ11 standard into general pinouts for use with the Pi's analogue
        read pins. These analogue sensors will be / are mounted upon the school's roof.
      </p>
      <p>
        From a programming standpoint, every step of the way has been a learning experience. Things which worked
        properly the day before suddenly don't work anymore for silly reasons. Probably the most common error made was
        with the stuff that I was comfortable with. It taught me a lesson, there; to not take my skill for granted. Mistakes happen to even the best coders, but sloppy mistakes are inexcusable.
      </p>
      <p>
        As a somewhat disappointing revelation, my first set of reed switch sensors were damaged, the cables apparently broken. I had to ship them back and recieve replacements, which should hopefully allow me to continue with the full goal of this project. If the new sensors work, you won't see this section!
      </p>
      <h4>Details of the Code</h4>
      <h5>Python</h5>
      <p>
        Having previous experience with Python code, I was comfortable using a Raspberry Pi 4 as the base for my sensor equipment. It was a familiar and easy language, and came with a Graphical User Interface that I much preferred over an Arduino IDE's look. It's also a full on computer, so that's helpful.
      </p>
      <p>
        I started with a simple Flask server, serving JSON over the internet to my own Web Application. I had to implement Flask CORS to allow a connection between the data server and the outdated HTTP protocol. I also needed to import the code library for my AdaFruit BME280 sensor package, so that I could recieve data from the module.
      </p>
      <!-- Make Sure To Hide Your Secrets! -->
      <p>
        From there, I connected my data server to OpenWeatherMap.org, an API that gave me sample data to serve alongside my own readings; things like the "Real Feel" temperature, and the sky conditions such as "Clear", "Cloudy", or "Snowing". Click <a href="https://api.openweathermap.org/data/2.5/weather?zip=16602,us&appid=431d09d780e3c761a8589f7bd5273fe0&units=imperial">HERE</a> to view the raw JSON response from OpenWeatherMap. To do this I had to import and use the "requests.get" function, which allowed me to request data from the API.
      </p>
      <p>
        Next I had to set up my RPi (Raspberry Pi) to work with my BME280 package. First I created my environment vairables for the hardwire connections and pinouts, those being the popular SPI connection, my digital read pin, and a combination of the two. Then I had to create a while loop, which would run forever. This allowed me to take readings at set intervals, using the "time.sleep" method. Once I had my vairables set up and my sensor hooked in, I could get to the fun stuff.
      </p>
      <p>
        I had to firstly rear each sensor for its data, which was straightforward enough. Variable X = reading on pin Y. Then I had to run some calculations. The temperature was in Celcius. That was okay, but Farhenheight is what I'm used to, so I added in the conversion as a math function. The pressure sensor output its reading in hPa, which was again fine, but PSI was a more relatable readout, so I had to figure out the conversion between hPa and PSI, which turned out to be a multiplication of hPa by 0.0145037738. After plugging that it, I now had my pressure readout in a helpful unit. Technically it should be in inches of mercury, but that's a more confusing way of seeing pressure, in my opinion. Next came my favorite challenge so far.
      </p>
      <p>
        This challenge was that of trying to calculate my altitude within a few meters, using only the air pressure sensor and a built-in calculation. But I had to figure out what the Sea Level Barometric pressure was for my location, and that's a bit nonsense. How do I measure the air pressure at sea level, when that's over 1,400 feet below ground? Well, after playing with it for a few days, I had what would be called a "Big Brain Moment". Why try to figure out the air pressure at sea level on a daily basis, when I could just add the difference in pressure from sea level to my altitude. This lead me on a search to find the difference, which lead me to a calculation used by pilots called the "Standard Day". This calculation is incredibly important, because it is how pilots adjust their altimeters. Without the calculation, a pilot would not know their altitude above sea level, which is used at all airports for runway elevation. If you're off by a few hundred feet, well, that doesn't end good.
      </p>
      <p>
        I had to make some assumtions here, since "Standard Day" was a very rare occurance. Did the ratio of pressure to altitude change depending on the conditions at sea level? You would assume so, but I assumed it did not for this use. As such, I found that the pressure difference between my altitude and sea level was 42.684hPa. I then took my pressure sensor reading, added the difference to it, and was plesantly surprised when, day after day, the altitude readout was accurate within 2 or 3 meters. So take that, science!... I guess? It brings up a big question why environmental variables do not change the rate of pressure difference.
      </p>
    </div>



    <FOOTER />
  </div>
  <!-- /container -->
</template>
<style scoped>
h5 {
  font-weight: bold;
}
h4 {
  font-weight: bold;
}

h3 {
  font-weight: bold;
}
p {
  font-style: italic;
}
</style>