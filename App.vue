<template>
  <div class="container">
    <div class="circle" :style="{ 'background': this.finalColor, 'transform':   this.transform }">
      <p v-if="inputValue < -10" class="text-light">Blue Star</p>
      <p v-else-if="inputValue > 10" class="text-light">Red Star</p>
      <p v-else class="text-secondary">Yellow Star</p>
    </div>
    <div class="top-left">
      <div class="d-flex align-items-center mb-5">
        <input v-model="inputValue" @change="changeColors();" @input="changeColors();" class="w-100" id="inputRange" type="range" :min="min" :max="max" step="5">
        <label class="ms-2" for="inputValue">{{ inputValue }}</label>
      </div>
      <div class="bottom-left">
        <label class="mb-2">Enter Velocity (km/s):</label>
        <input v-model="velocity" @change="velocityControl" class="form-control" placeholder="Enter velocity.." type="text">
      </div>
      <div>
        <a class="btn btn-secondary top-right" target="_blank" href="https://github.com/rubanero14/Vue-Tests-Doppler-Effect">Source Code</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      inputValue: 0,
      velocity: 0,
      min: -100,
      max: 100,
      red: 0,
      green: 0,
      blue: 255,
      finalColor: '',
      transform: 0,
    };
  },
  methods: {
    velocityControl(){
      if(this.velocity < this.min){
        this.min = -100;
        this.velocity = this.min;
      } else if(this.velocity > this.max){
        this.max = 100;
        this.velocity = this.max;
      } else {
        this.inputValue = parseInt(this.velocity);
        console.log(typeof this.inputValue, this.inputValue);
      }
    },
  },
  watch: {
    inputValue: function changeColors(){
      if (this.inputValue < 0){
        this.red = 255 + (this.inputValue * 2.55);
        this.blue = -(this.inputValue * 2.55);
        this.green = 255 + (this.inputValue * 2.55);
        this.finalColor = 'rgb('+ this.red + ',' + this.green + ',' + this.blue + ')';
        this.transform = 'scale('+(2.5 - this.inputValue*0.015)+')';
        console.log('blue activated');
        console.log('Final color '+this.finalColor);
        console.log('Green '+this.green);
        console.log('Red '+this.red);
        console.log('Blue '+this.blue);
        console.log('Transform '+this.transform);
      } else if (this.inputValue > 0){
        this.red = 255;
        this.green = 255 - (this.inputValue * 2.55);
        this.blue = 0;
        this.finalColor = 'rgb('+ this.red + ',' + this.green + ',' + this.blue + ')';
        this.transform = 'scale('+(2.5 + this.inputValue*(-0.015))+')';
        console.log('red activated');
        console.log('Final color '+this.finalColor);
        console.log('Green '+this.green);
        console.log('Red '+this.red);
        console.log('Blue '+this.blue);
        console.log('Transform '+this.transform);
        console.log('inputvalue '+this.inputValue);
      } else {
        this.green = 255 - (this.inputValue * 2.55);
        this.red = 255;
        this.blue = 0;
        this.finalColor = 'rgb('+ this.red + ',' + this.green + ',' + this.blue + ')';
        this.transform = 'scale('+(2.5 + this.inputValue*0.015)+')';
        console.log('yellow activated');
        console.log('Final color '+this.finalColor);
        console.log('Green '+this.green);
        console.log('Red '+this.red);
        console.log('Blue '+this.blue);
        console.log('Transform '+this.transform);
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

.top-right {
  position: fixed;
  top: 20px;
  right: 20px;
}

.bottom-left {
  position: fixed;
  bottom: 20px;
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
  transition: all 0.3s ease-in-out;
}

.circle {
  height: 150px;
  width: 150px;
  border: 1px solid #ccc;
  border-radius: 100%;
  margin: 40vh auto;
  transition: all 0.3s ease-in-out;
  background: rgb(255,255,0);
  transform: scale(2.5);
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
