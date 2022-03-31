<template>
  <header>
      <h1 class="mb-0">Doppler Effect Demo</h1>
  </header>
  <div class="container">
    <div class="circle" :style="{ 'background': this.finalColor, 'transform':   this.transform }">
      <p v-if="inputValue < -10" class="text-light">Blue Star</p>
      <p v-else-if="inputValue > 10" class="text-light">Red Star</p>
      <p v-else class="text-secondary">Yellow Star</p>
    </div>
  </div>
  <footer class="my-3">
    <div class="container">
      <div class="row">
        <div class="col-12 col-md-6 col-lg-4">
          <input v-model="inputValue" @change="changeColors();" @input="changeColors();" class="w-100 mb-3 mb-md-0" id="inputRange" type="range" :min="min" :max="max" step="5">
        </div>
        <div class="col-12 col-md-6 col-lg-4">
          <div class="d-flex align-items-center">
              <label class="mb-3 mb-md-0 me-2">Enter Velocity (km/s):</label>
              <input v-model="velocity" @change="velocityControl" class="form-control w-auto mb-3 mb-md-0" type="number">
          </div>
        </div>
        <div class="col-12 col-md-6 col-lg-4">
          <a class="btn btn-secondary w-100" target="_blank" href="https://github.com/rubanero14/Vue-Tests-Doppler-Effect">Source Code</a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  data(){
    return {
      inputValue:'',
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
      } else if(this.velocity == ''){
        this.velocity = 0;
      } else {
        this.inputValue = this.velocity;
        console.log(typeof this.inputValue, this.inputValue);
      }
    },
  },
  watch: {
    inputValue: function changeColors(){
      this.velocity = parseInt(this.inputValue);
      if (this.inputValue < 0){
        this.red = 255 + (this.inputValue * 2.55);
        this.blue = -(this.inputValue * 2.55);
        this.green = 255 + (this.inputValue * 2.55);
        this.finalColor = 'rgb('+ this.red + ',' + this.green + ',' + this.blue + ')';
        this.transform = 'scale('+(2.3 - this.inputValue*0.015)+')';
      } else if (this.inputValue > 0){
        this.red = 255;
        this.green = 255 - (this.inputValue * 2.55);
        this.blue = 0;
        this.finalColor = 'rgb('+ this.red + ',' + this.green + ',' + this.blue + ')';
        this.transform = 'scale('+(2.5 + this.inputValue*(-0.015))+')';
      } else {
        this.green = 255 - (this.inputValue * 2.55);
        this.red = 255;
        this.blue = 0;
        this.finalColor = 'rgb('+ this.red + ',' + this.green + ',' + this.blue + ')';
        this.transform = 'scale('+(2.5 + this.inputValue*0.015)+')';
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

header {
  margin: 30px auto;
  text-align: center;
}

footer {
  margin: 30px auto;
  text-align: center;
}

.top-left {
  position: fixed;
  top: 20px;
  left: 20px;
}

.bottom-right {
  position: fixed;
  bottom: 20px;
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
  margin: 30vh auto;
  transition: all 0.3s ease-in-out;
  background: rgb(255,255,0);
  transform: scale(2.5);
}

@media (max-width: 992px){
  .circle {
    height: 100px;
    width: 100px;
    margin: 30vh auto;
  }
  
  p {
    margin: 37px auto;
    text-align: center;
  }
}
</style>
