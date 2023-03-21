<template>
  <div :class="weather.temperature >= 16 ? 'hot' : 'cold'">
    <div id="weather">
      <input
        type="text"
        placeholder="Search..."
        class="input-search"
        v-model="inputSearch"
        @keyup.enter="getWeather"
      />
      <div class="content">
        <h1 class="name">
          <span class="city">{{ weather.city }}</span>
          <span>, </span>
          <span class="country">{{ weather.country }}</span>
        </h1>
        <p class="time">{{ time }}</p>
        <div class="temperature">
          <span class="value">{{ weather.temperature }}</span>
          <span><sup>o</sup>C</span>
        </div>
        <div class="short-desc">{{ weather.shortDesc }}</div>
        <div class="more-desc">
          <div class="visibility">
            <i class="far fa-eye"> {{ " " + weather.visibility + " (m)" }}</i>
            <span></span>
          </div>
          <div class="wind">
            <i class="fas fa-wind"> {{ " " + weather.wind + " (m/s)" }}</i>
            <span></span>
          </div>
          <div class="cloud">
            <i class="fas fa-cloud-sun">{{ " " + weather.cloud + " (%)" }}</i>
            <span></span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "WeatherComponent",
  data() {
    return {
      inputSearch: "Ha Noi",
      apiKey: "d78fd1588e1b7c0c2813576ba183a667",
      urlBase: "https://api.openweathermap.org/data/2.5/",
      weather: {
        city: "",
        country: "",
        temperature: "",
        shortDesc: "",
        visibility: "",
        wind: "",
        cloud: "",
      },
      time: new Date().toLocaleString(),
    };
  },
  mounted: function () {
    this.getWeather(this.inputSearch);
  },
  methods: {
    getWeather() {
      const url = `${this.urlBase}weather?q=${this.inputSearch}&units=metric&appid=${this.apiKey}`;
      fetch(url)
        .then((res) => {
          return res.json();
        })
        .then(this.changeWeather);
    },
    changeWeather(result) {
      if (result !== null && result !== "udefined") {
        this.weather = {
          city: result.name,
          country: result.sys.country,
          temperature: Math.round(result.main.temp),
          shortDesc: result.weather[0].description,
          visibility: result.visibility,
          wind: result.wind.speed,
          cloud: result.clouds.all,
        };
      }
    },
  },
};
</script>

<style>
@import url("https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta2/css/all.min.css");
#app {
  background-image: url("../assets/warm-bg.jpg");
}
.hot {
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 1)),
    url(../assets/warm-bg.jpg) no-repeat center/cover;
}

.hot #weather {
  background-image: url(../assets/warm-bg.jpg);
}

.cold {
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0.7), rgba(0, 0, 0, 1)),
    url(../assets/cold-bg.jpg) no-repeat center/cover;
}

.cold #weather {
  background-image: url(../assets/cold-bg.jpg);
}

#weather {
  min-width: 350px;
  height: 600px;
  background: no-repeat center/cover;
  text-align: center;
  padding: 30px 20px;
  border-radius: 10px;
  transition: 0.4s;
}

#weather input {
  padding: 10px 20px;
  background-color: rgba(255, 255, 255, 0.4);
  font-size: 19px;
  box-shadow: 0 5px 4px rgba(0, 0, 0, 0.2);
  border: none;
  outline: none;
  border-radius: 0px 15px 0 15px;
  margin-bottom: 40px;
  width: 100%;
  transition: 0.4s;
}

#weather input:focus {
  background-color: rgba(255, 255, 255, 0.8);
  border-radius: 15px 0 15px 0;
}

#weather .content {
  color: white;
}

#weather .content .name {
  white-space: nowrap;
  font-size: 35px;
  text-shadow: 2px 2px rgba(0, 0, 0, 0.5);
}

#weather .content .time {
  font-size: 15px;
  margin: 6px 0;
}

#weather .content .temperature {
  font-size: 65px;
  text-shadow: 4px 4px rgba(0, 0, 0, 0.6);
  display: inline-block;
  padding: 20px;
  background-color: rgba(255, 255, 255, 0.4);
  border-radius: 15px;
  box-shadow: 2px 2px 0 2px rgba(0, 0, 0, 0.5);
  margin: 20px 0 30px;
  font-weight: 800;
}

#weather .content .short-desc {
  font-size: 40px;
  font-weight: 600;
  text-shadow: 3px 3px rgba(0, 0, 0, 0.4);
}

#weather .content .more-desc {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 40px;
}

#weather .content .more-desc > div {
  font-size: 16px;
  display: flex;
  flex-direction: column;
}

#weather .content .more-desc > div span {
  margin-top: 15px;
}
</style>
