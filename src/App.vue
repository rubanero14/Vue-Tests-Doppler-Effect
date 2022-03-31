<template>
  <header>
      <h1 class="mb-0"><i class="bi bi-stars me-2"></i>Doppler Effect Demo<i class="bi bi-stars ms-2"></i></h1>
  </header>
  <div class="container">
    <div class="circle" @click="reset" :style="{ 'background': this.finalColor, 'transform':   this.transform }"></div>
  </div>
  <footer class="my-3">
    <div class="container">
      <div class="row">
        <div class="col-12 col-md-6 col-lg-4">
          <div class="d-flex align-items-center justify-content-between">
            <label class="me-2">-100</label>
            <input v-model="inputValue" @change="changeColors();" @input="changeColors();" 
              class="w-100 mb-3 mb-md-0" id="inputRange" type="range" :min="min" :max="max" step="5">
            <label class="ms-2">100</label>
          </div>
        </div>
        <div class="col-12 col-md-6 col-lg-4">
          <div class="d-flex align-items-center">
              <label class="mb-3 mb-md-0 me-2">Enter Velocity (km/s):</label>
              <input v-model="inputValue" @input="changeColors();"
              class="form-control w-auto mb-3 mb-md-0" type="number">
          </div>
        </div>
        <div class="col-12 col-md-6 col-lg-4">
          <a class="btn btn-secondary w-100" target="_blank" href="https://github.com/rubanero14/Vue-Tests-Doppler-Effect">
            <i class="bi bi-code-slash me-2"></i>Source Code
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  data(){
    return {
      inputValue: 0,
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
    changeColors(){
      // To set boundary for min and max value to be inputted in input.form-control
      if(this.inputValue < this.min){
          this.inputValue = this.min;
        } else if(this.inputValue > this.max){
          this.inputValue = this.max;
        }

      // Logic for setting background and scale size based on input value
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
    reset(){
      this.inputValue = 0;
      this.finalColor = '';
      this.transform = null;
    },
  },
}
</script>

<style>
@import url('https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css');
@import url("https://cdn.jsdelivr.net/npm/bootstrap-icons@1.8.1/font/bootstrap-icons.css");

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

label {
 display: inline-block;
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
}
</style>
