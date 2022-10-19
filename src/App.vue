<template>
  <div class="container-sm col-sm-4" id="app">
    <UserForm
      v-if="state === 0"
      @submitted="
        setProps($event);
        setState();
        fetchLocation();
      "
    />
    <CameraSnap
      v-if="state === 1"
      @picture-taken="
        setState();
        fetchWeather();
        imageSrc = $event;
      "
    />

    <img v-if="state === 2" class="rounded-5" :src="imageSrc" />
    <div class="d-flex justify-content-around m-3">
      <p class="h3" v-if="state === 2">{{ name }}</p>
      <p class="h3" v-if="state === 2">{{ city }}</p>
    </div>

    <Table v-if="state === 2" :data="dailyWeather" />
    <b-button
      class="m-5"
      v-if="state === 2"
      type="is-primary"
      @click="
        () => {
          this.state = 0;
        }
      "
      >Restart
    </b-button>
  </div>
</template>

<script>
import CameraSnap from "./components/CameraSnap.vue";
import UserForm from "./components/UserForm.vue";
import Table from "./components/Table.vue";

export default {
  name: "App",
  components: {
    CameraSnap,
    UserForm,
    Table,
  },
  methods: {
    toast() {
      this.$buefy.toast.open({
        type: "is-danger",
        message: "Request Failed!",
      });
    },
    setState() {
      this.state++;
      console.log(this.city, this.name, this.state);
      console.log(this.dailyWeather, this.weather);
    },
    setProps(props) {
      this.name = props.name;
      this.city = props.city;
      console.log(this.city, this.name, this.state);
    },
    fetchLocation() {
      if (this.state === 1) {
        fetch(
          `http://api.openweathermap.org/geo/1.0/direct?q=${this.city}&appid=30a97f591964e0ca08c7bf10847c4f07`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setGeoResult)
          .catch((error) => {
            console.error(error);
            this.toast();
          });
      }
    },
    fetchWeather() {
      if (this.state === 2) {
        fetch(
          `http://api.openweathermap.org/data/2.5/forecast?lat=${this.location.lat}&lon=${this.location.lon}&appid=30a97f591964e0ca08c7bf10847c4f07&units=metric`
        )
          .then((res) => {
            return res.json();
          })
          .then((res) => {
            this.setWeatherResult(res);
          })
          .catch((error) => {
            console.error(error);
            this.toast();
          });
      }
    },
    setGeoResult(result) {
      this.location = JSON.parse(JSON.stringify(result[0]));
      console.log(this.location);
    },
    setWeatherResult(result) {
      console.log(result);
      this.weather = result;
      console.log(this.weather.list);
      for (let i = 0; i < this.weather.list.length; i = i + 8) {
        this.dailyWeather.push(this.weather.list[i]);
      }
      console.log(this.dailyWeather);
    },
  },
  data() {
    return {
      imageSrc: null,
      state: 0,
      name: "",
      city: "",
      location: {},
      weather: {},
      dailyWeather: [],
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
