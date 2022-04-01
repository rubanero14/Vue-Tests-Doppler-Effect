<template>
  <section :class="{ dark: darkMode }">
    <header>
        <h1 class="mb-0"><i class="bi bi-stars me-2"></i>Doppler's Effect Demo<i class="bi bi-stars ms-2"></i></h1>
        <transition name="flip-side" mode="out-in">
            <button v-if="darkMode" @click="darkModeControl" class="btn btn-secondary btn-rounded">
              <i class="bi bi-brightness-high"></i>
            </button>
            <button v-else @click="darkModeControl" class="btn btn-secondary btn-rounded">
              <i class="bi bi-moon"></i>
            </button>
        </transition>
    </header>
    <div class="container">
      <div class="circle" @click="reset" :style="{ 'background': this.backgroundColor, 'transform': this.transform }"></div>
    </div>
    <footer>
      <div class="container">
        <div class="row">
          <div class="col-12 col-md-4 order-1 order-md-2">
            <div class="d-flex align-items-center justify-content-between mb-3 mb-md-0">
              <label class="me-2">-100</label>
              <input v-model="inputValue" @input="changeColors();" 
                class="w-100" type="range" :min="min" :max="max" step="5">
              <label class="ms-2">100</label>
            </div>
          </div>
          <div class="col-12 col-md-4 order-2 order-md-1">
            <div class="d-flex align-items-center justify-content-center">
                <label class="mb-3 mb-md-0 me-2">Enter Velocity (km/s):</label>
                <input v-model="inputValue" @input="changeColors();"
                class="form-control text-center w-25 mb-3 mb-md-0" type="number">
            </div>
          </div>
          <div class="col-12 col-md-4 order-3">
            <a class="btn btn-secondary w-100" target="_blank" href="https://github.com/rubanero14/Vue-Tests-Doppler-Effect">
              <i class="bi bi-code-slash me-2"></i>Source Code
            </a>
          </div>
        </div>
      </div>
    </footer>
  </section>
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
      backgroundColor: '',
      transform: 'scale(2.5)',
      darkMode: false,
    };
  },
  methods: {
    changeColors(){
      // To set boundary for min and max value to be inputted in input.form-control
      if (this.inputValue < this.min){
          this.inputValue = this.min;
        } else if (this.inputValue > this.max){
          this.inputValue = this.max;
        }

      // To set background color and scale size based on input value
      if (this.inputValue < 0){
        this.red = 255 + (this.inputValue * 2.55);
        this.blue = -(this.inputValue * 2.55);
        this.green = 255 + (this.inputValue * 2.55);
        this.backgroundColor = 'rgb('+ this.red + ',' + this.green + ',' + this.blue + ')';
        this.transform = 'scale('+(2.3 - this.inputValue*0.015)+')';
      } else if (this.inputValue > 0){
        this.red = 255;
        this.green = 255 - (this.inputValue * 2.55);
        this.blue = 0;
        this.backgroundColor = 'rgb('+ this.red + ',' + this.green + ',' + this.blue + ')';
        this.transform = 'scale('+(2.5 + this.inputValue*(-0.015))+')';
      } else {
        this.green = 255 - (this.inputValue * 2.55);
        this.red = 255;
        this.blue = 0;
        this.backgroundColor = 'rgb('+ this.red + ',' + this.green + ',' + this.blue + ')';
        this.transform = 'scale('+(2.5 + this.inputValue*0.015)+')';
      }
    },
    darkModeControl(){
      // to toggle dark mode view
      return this.darkMode = !this.darkMode;
    },
    reset(){
      // to reset circle's state back to original state
      this.inputValue = 0;
      this.backgroundColor = '';
      this.transform = 'scale('+(2.5 + this.inputValue*0.015)+')';  
    },
  },
}
</script>

<style>
@import url('https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css');
@import url('https://cdn.jsdelivr.net/npm/bootstrap-icons@1.8.1/font/bootstrap-icons.css');
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@100;300;400;500&display=swap');

section {
  box-sizing: border-box;
  background: #ccc;
  font-family: 'Roboto', sans-serif;
  font-weight: 500;
  font-size: 13px;
  color: #333;
  padding: 20px;
  transition: all 0.3s ease-in-out;
  height: 100vh;
}

header {
  margin: 30px auto ;
  text-align: center;
}

h1 {
  font-size: 30px;
}

footer {
  margin: 30px auto 0;
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
}

.bi-brightness-high::before, .bi.bi-moon::before {
    color: #ccc;
}

.btn-secondary:focus, .btn-secondary:focus-visible, .btn-secondary:active:focus {
  border-color: none;
  box-shadow: 0 1px 4px 0 rgb(0, 0, 0, 0.5);
}

.btn-rounded {
  position: fixed;
  top: 30px;
  right: 30px;
  height: 40px;
  width: 40px;
  border-radius: 100%;
  padding: 0;
}

.flip-side-enter-from, .flip-side-leave-to {
  opacity: 0;
  transform: rotateY(180deg);
}
.flip-side-enter-active, .flip-side-leave-active {
  transition: all 0.5s ease-out;
}
.flip-side-enter-to, .flip-side-leave-from {
  opacity: 1;
  transform: rotateY(0deg);
}

/* Dark Mode */
section.dark {
  background: #333;
  color: #ccc;
} 

.dark .circle {
  border: 1px solid #333;
} 

@media (max-width: 992px){
  .circle {
    height: 100px;
    width: 100px;
    margin: 25vh auto;
  }

  h1 {
    font-size: 25px;
  }

  .btn-rounded {
    position: fixed;
    top: 10px;
    right: 10px;
  }
}
</style>
