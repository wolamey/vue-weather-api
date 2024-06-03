<script>
import axios from 'axios';


export default {
  data() {
    return {
      city: "",
      error: "",
      info: null,
    }
  },
  computed: {
    cityName() {
      return ` '${this.city}' `
    },

    weatherDescription(){
      return`Описание: ${this.info.weather[0].description}`
    }

  },
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = 'Название должно быть более чем 2 символа'
        return false
      }
      this.error = ''
      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=19bc74efbd0e229bf500a5e1349e242b`)
      .then(res => (this.info = res.data))
    }
  }
}
</script>




<template>

  <div class="wrapper">
    <h1>Погода</h1>
    <p>узнать погоду в {{ city == "" ? "вашем городе" : cityName }}</p>

    <input type="text" placeholder="Введите ваш город" v-model="city">
    <button v-if="city !== ''" @click="getWeather()">Узнать погоду</button>
    <button v-else disabled>Введите название города</button>


    <p class="error"> {{ error }} </p>


    <p v-if="info != null">{{ weatherDescription }}</p>
  </div>

</template>




<style scoped>
.wrapper {
  border-radius: 30px;
  background-color: rgba(255, 255, 255, 0.796);
  border: 1px black solid;
  padding: 40px;
  text-align: center;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;

}

.wrapper input {
  padding: 10px;
  background-color: transparent;
  width: 100%;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  border: none;
  border-bottom: 1px black solid;
  outline: none;
  margin: 30px 0
}

.wrapper button {
  background-color: transparent;
  border-radius: 10px;
  border: 1px black solid;
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  padding: 10px;
  cursor: pointer;
  transition: 0.3s;
}

.wrapper button:hover {
  scale: 1.1;
}


.wrapper button:disabled {
  cursor: not-allowed;
}

.error{
  color: red;
  margin: 20px 0 00 0;
}
</style>