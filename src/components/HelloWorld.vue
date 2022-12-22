<template>
  <div>
    <div class="container-fluid p-0 m-0">
      <div class="row">
        <div class="col-lg-8 ms-5">
          <b-input-group class="mt-3 w-50">
            <b-form-input type="search" v-model="searchcity" placeholder="Enter City Name"></b-form-input>
            <b-input-group-append>
              <b-button variant="outline-success" @click="getdata()">Search</b-button>
            </b-input-group-append>
          </b-input-group>
          <div>
            <div class="weather-data">
              <div>
                <h1 class="city">{{ this.city }}</h1>
                <small class="rain">{{ this.rain }}</small>
                <p class="condition">{{ this.description }}</p>
                <h5 class="temp">
                  <v-icon color="#FF0000" class="mr-2" size="40">mdi-thermometer-high</v-icon>{{ this.temp
                  }}<span>&#176;</span>
                </h5>
              </div>
              <div>
                <img class="img" v-bind:src="this.imgsrc" />
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
  name: "HelloWorld",
  data() {
    return {
      time: "",
      citie: "",
      searchcity: "",
      imgsrc: "",
      rain:'',
      city: "",
      temp: "",
      description: "",
      pressure: "",
      humidity: "",
      visibility: "",
      right: null,
    };
  },
  mounted() {
    fetch(
      "https://api.openweathermap.org/data/2.5/weather?q=Lahore&appid=306807ad7cfa2516d41e3318086b059d"
    )
      .then((response) => response.json())
      .then((data) => {
        this.time = new Date(data.dt * 1000 + data.timezone * 1000);
        this.city = data.name;
        this.temp = Math.round(data.main.temp_max - 273.15);

        this.description = data.weather[0].description;
        this.pressure = data.main.pressure;
        this.humidity = data.main.humidity;
        this.visibility = data.visibility;
        this.imgsrc = `https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`;
      });
  },
  methods: {
    getdata() {
      console.log(this.searchcity);
      fetch(
        `https://api.openweathermap.org/data/2.5/weather?q=${this.searchcity}&appid=306807ad7cfa2516d41e3318086b059d`
      )
        .then((response) => response.json())
        .then((data) => {
          this.time = new Date(data.dt * 1000 + data.timezone * 1000);
          this.city = data.name;
          this.temp = Math.round(data.main.temp_max - 273.15);

          this.description = data.weather[0].description;
          this.pressure = data.main.pressure;
          this.humidity = data.main.humidity;
          this.visibility = data.visibility;
          this.imgsrc = `https://openweathermap.org/img/wn/${data.weather[0].icon}@2x.png`;
        });
    },
  },
};
</script>
<style scoped>
.temp {
  margin-top: 20px;
  font-size: 28px;
}
.img {
  height: 100px;
  width: 100px;
}

.city-name {
  font-size: 16px;
  color: black;
  cursor: pointer;

  margin-left: 10px;
  margin-right: 10px;
  margin-top: 5px;
}
.city-name:hover {
  background-color: black;
  color: white;
  border-radius: 10px;
}

.list {
  background-color: #eaecef !important;
  text-align: center;
  margin-top: 60px;
  height: 690px;
  margin-right: 10px;
  border-radius: 10px;
  overflow: scroll;
  overflow-x: hidden;
}

.city {
  font-size: 32px;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: bold;
}

.condition {
  font-size: 26px;
  font-family: Arial, Helvetica, sans-serif;
}

.icon {
  color: black;
  margin-left: 20px;
  font-family: Arial, Helvetica, sans-serif;
  font-weight: bold;
}

.name {
  color: grey;
}

.weather-more-data {
  padding: 20px;
  background-color: #eaecef;
  margin-top: 20px;
  display: flex;
  justify-content: space-evenly;
  border-radius: 10px;
}

.weather-data {
  width: 50%;
  padding: 20px;
  border: 1px solid black;
  margin-top: 20px;
  display: flex;
  justify-content: space-between;
  border-radius: 10px;
}
</style>
