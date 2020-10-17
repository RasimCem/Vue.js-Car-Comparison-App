<template>
  <div>
    <h1 class="text">Car Comparison App</h1>
    <div class="container">
        <first-car @clear="clean" :results="result" @first="firstSelect($event)" :car="cars"></first-car>
        <second-car  @clear="clean" :results="result" @second="secondSelect($event)" :car="cars"></second-car>
    </div>
        <button @click="compare">Let's Compare!</button>
  </div>
</template>

<script>
import FirstCar from './components/FirstCar.vue'
import SecondCar from './components/SecondCar.vue'
export default {
  name: 'App',
  components: {
    FirstCar,
    SecondCar
  },
  data(){
    return{
      cars:[],
      firstSelected:'',
      secondSelected:'',
      result:
        {
          yearWinner:"",
          powerWinner:"",  
          priceWinner:""
        }
    
    }
  },
  mounted() {
    this.fetchCars();
  },
  methods: {
    fetchCars(){
      fetch("http://private-anon-0f7aa438b4-carsapi1.apiary-mock.com/cars")
      .then(response => response.json())
      .then(data => this.cars=data);
    },
    firstSelect(event){
      this.firstSelected=''
      this.firstSelected=event
    },
    secondSelect(event){
      this.secondSelected=''
      this.secondSelected=event
    },
    compare(){
      if(this.firstSelected.length === 0 || this.secondSelected.length === 0 ){
        alert("You didn't choose car!")
      }
      else{
          if(this.firstSelected.year > this.secondSelected.year){
            this.result.yearWinner="first"
          }
          else if(this.firstSelected.year < this.secondSelected.year){
            this.result.yearWinner="second"
          }
          if(this.firstSelected.horsepower > this.secondSelected.horsepower){
            this.result.powerWinner="first"
          }
          else if(this.firstSelected.horsepower < this.secondSelected.horsepower){
            this.result.powerWinner="second"
          }
          if(this.firstSelected.price > this.secondSelected.price){
            this.result.priceWinner="second"
          }
          else if(this.firstSelected.price < this.secondSelected.price){
            this.result.priceWinner="first"
          }
          
      } 
   
    },
    clean(){
      this.result.yearWinner=null,
      this.result.priceWinner=null,
      this.result.powerWinner=null
    }

  },

}
</script>

<style>
#app {

}
div{
  margin: auto auto;
}
.text{
  color: #fff;
  letter-spacing: 1px;
  word-spacing: 3px;
  margin-top: 75px;
  text-align: center;
}
.container {
  width: 70%;
  height: 500px;
  margin-top: 50px;
  display: flex;
  background-color: #B5D3FB;
  justify-content: space-between;
  padding: 25px;
  border-radius: 5px;
}
button{
  display: block;
  margin: 50px auto;
  width: 25%;
  padding: 15px;
  border-radius: 8px;
  border:none;
  outline: none;
  cursor: pointer;
  font-size: 17px;
  background-color: #B5F7FB;
  letter-spacing: 2px;
}
button:hover{
  background-color:#55C3C8 ;
  transition: .4s;
}

</style>
