<template>
  <div class="container">
    <div class="circle" :style="{ 'background': this.finalColor, 'transform': this.transform }">
      <p v-if="this.inputValue < 0">Sun</p>
      <p v-else-if="this.inputValue == 0">Giant Sun</p>
      <p v-else>Red Giant</p>
    </div>
    <div class="top-left">
      <div class="d-flex align-items-center mb-5">
        <input v-model="inputValue" @input="changeColors();" class="w-100" id="inputRange" type="range" :min="min" :max="max" step="5">
        <label class="ms-2" for="inputValue">{{ inputValue }}</label>
      </div>
      <div>
        <label class="mb-2">Enter Velocity (km/s):</label>
        <input v-model="velocity" @change="velocityControl" class="form-control" placeholder="Enter velocity.." type="text">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      inputValue: -100,
      velocity: 0,
      min: -100,
      max: 100,
      green: 255,
      yellow: 'rgb(255,255,0)',
      finalColor: '',
      transform: 0,
    };
  },
  methods: {
    changeColors(){
      if (this.inputValue < 0){
        this.green = 165 - (this.inputValue * 0.9);
        this.finalColor = 'rgb(255,'+this.green+',0)';
        this.transform = 'scale('+(2.5 - this.inputValue*(-0.015))+')';
        console.log('orange activated');
        console.log('Final color '+this.finalColor);
        console.log('Green '+this.green);
        console.log('Transform '+this.transform);
      } else if (this.inputValue > 0){
        this.green = 165 - (this.inputValue * 1.65);
        this.finalColor = 'rgb(255,'+this.green+',0)';
        this.transform = 'scale('+(1.5 + this.inputValue*0.015)+')';
        console.log('red activated');
        console.log('Final color '+this.finalColor);
        console.log('Green '+this.green);
        console.log('Transform '+this.transform);
      } else {
        this.green = 165;
        this.finalColor = this.yellow; 
        console.log('yellow activated');
        console.log('Final color '+this.finalColor);
        console.log('Green '+this.green);
        console.log('Transform '+this.transform);
      }
    },
    velocityControl(){
      if(this.velocity < this.min){
        this.min = -100;
        this.velocity = this.min;
      } else if(this.velocity > this.max){
        this.max = 100;
        this.velocity = this.max;
      } else {
        this.inputValue = this.velocity;
      }
    },
  },
}
</script>

<style>
@import url('https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css');
body {
  box-sizing: border-box;
  background: #ccc;
}

.top-left {
  position: fixed;
  top: 20px;
  left: 20px;
}

label {
 display: inline-block;
}

.center {
  margin: 300px auto;
}

p {
  margin: 60px auto;
  text-align: center;
}

.circle {
  height: 150px;
  width: 150px;
  border: 1px solid #ccc;
  border-radius: 100%;
  margin: 40vh auto;
  transition: all 0.3s ease-in-out;
  background: yellow;
}

@media (max-width: 992px){
  .circle {
    height: 100px;
    width: 100px;
  }
  
  p {
    margin: 37px auto;
    text-align: center;
  }
}
</style>
