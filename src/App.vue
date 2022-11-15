<template>
  <div
    id="app"
    :class="
      typeof answer.current != 'undefined' && answer.current.feelslike_c > 16
        ? 'warm'
        : ''
    "
  >
    <div class="container">
      <div class="search-box">
        <input
          class="search-bar"
          placeholder="Например Landon"
          type="text"
          v-model="city"
          v-on:keydown.enter="ws(city)"
        />
      </div>

      <div v-if="answer" class="main">
        <div class="location-box">
          <div class="location">
            {{ answer.location.name }} , {{ answer.location.region }} ,
            {{ answer.location.country }}
          </div>
          <div class="date">{{ answer.current.last_updated }}</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{ answer.current.feelslike_c }}°c</div>
          <div class="weather">{{ answer.current.condition.text }}</div>
          <div class="weather">Wind: {{ answer.current.wind_kph }} kph</div>
        </div>
      </div>
      <div v-else>
        <div class="weather-box">
          <div class="temp1">
            made by VLV , <br />
            search something
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      city: "",
      answer: "",
    };
  },
  methods: {
    ws(city) {
      fetch(
        `https://api.weatherapi.com/v1/current.json?key=f846d5433b094284b9a73745221511&q=${city}&aqi=no`
      )
        .then((response) => response.json())
        .then((response) => (this.answer = response))
        .then(() => console.log(this.answer))
        .catch((err) => console.error(err));
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "montserrat", sans-serif;
}

#app {
  background-image: url("./assets/damien-schnorhk-Vqx-e9esWZk-unsplash.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: 50% 50%;
  height: 100vh;
}
#app .warm {
  background-image: url(./assets/taryn-kaahanui-AOa-SkDREDE-unsplash.jpg);
}
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding-top: 10vh;
}

.search-box {
  width: 20%;
  margin-bottom: 30px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}
.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .temp1 {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 20px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
