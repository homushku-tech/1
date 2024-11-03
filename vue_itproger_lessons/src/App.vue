<template>
    <!-- <input type="text" v-model="userName" placeholder="Имя">
    <input type="password" v-model="userPass" placeholder="Пароль">
    <input type="email" v-model="userEmail" placeholder="Почта">
    <p>{{ error }}</p>
    <button @click="sendData()">Отправить</button>
    <!-- оператор ветвления для vue.js -->
    <!-- <div v-if="users.length == 0" className="user">
      У нас нет пользователей
    </div>
    <div v-else-if="users.length == 1" className="user">
      У нас один пользователь
    </div>
    <div v-else  className="user">
      У нас более одного пользователя
    </div> -->
    <!-- прием и передача объектов от компоненты User -->
    <!-- <User v-for="(el, index) in users" :key="index" :user="el" :index="index" :deleteUser="deleteUser"/>  -->
    <div class = "wrapper">
            <h1>Погодное приложение</h1>
            <p>Узнать погоду в {{ city =="" ? "вашем городе" : cityName }}</p>
            <input type="text" v-model="city" placeholder="Выберите город">
            <button v-if = "city != '' " @click ="getWeather() "> Получить погоду </button>
            <button disabled v-else> Введите название города </button>
            <p class="error"> {{ error }} </p>
            <p> {{ showTemp}} </p>
    </div>
</template>


<script>
    import axios from 'axios'
    export default {
          data(){
              return{
                city: "",
                error: "",
                info: "",
              }
          },
          computed: {
            cityName(){
                    return this.city
            },
            showTemp(){
                    return "Температура: " + this.info.main.temp
            },
            showFeelsLike(){
                    return "Ощущаемая температура: " + this.info.main.feels_like
            },
            
            showTempMin(){
                    return "Минимальная температура: " + this.info.main.temp_min
            },
            
            showTempMax(){
                    return "Максимальная температура: " + this.info.main.temp_max
            },
          },
          methods:{
            getWeather(){
                    if (this.city.trim().length < 2 ){
                      this.error = "Нужно название более одного символа"
                      return false
                    }
                    this.error = ""

                    axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=7fae2867732b2c4d0f9917c1b9c36665`)
                     .then(res => (this.info = res.data))             
                  }
          },
    } 
// import User from './components/User.vue'  /*вот так мы импортируем компоненты */

//   export default {
//       components: { User },
//       data(){
//           return{
//             users: [],
//             error: '',
//             userName: '',
//             userPass: '',
//             userEmail: ''
//           }
//       },
//       methods: {
//         sendData(){
//             if (this.userName == '') {
//                 this.error = "Имя не введено"
//                 return;
//             }else if (this.userPass == '') {
//                 this.error = "Пароль не введено"
//                 return;
//             }else if (this.userEmail == '') {
//                 this.error = "Почта не введено"
//                 return;
//             }
//             this.users.push({    
//                 name: this.userName,
//                 pass: this.userPass,
//                 email: this.userEmail
//             })
//         },
//         deleteUser(index){
//                this.users.splice(index, 1); //удаление из массива
//         }

//       }

//   }
</script>

<style scoped>
.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  background-color: #1f0f24;
  padding: 20px;
  text-align: center;
  color: #fff;
}
.wrapper h1{
  margin-top: 50px;
}
.wrapper p{
  margin-top: 20px;
}
.wrapper input {
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid #110813;
    color: #fcfcfc;
    font-size: 14px;
    padding: 5pz 8px ;
    outline: none;
}
.wrapper input:focus{
    border-bottom-color: #6e2d7d;
}
.wrapper button:disabled{
  background: #9f0606d2;
}
.wrapper button{
  background: #e3bc4b;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}
.wrapper button:hover {
  transform: scale(1.1) translateY(-5px);
}
/* input{
  display: block  
} */
</style>
