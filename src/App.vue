<template>
  <div class="container">
    <div class="circle" :class="{ 'red' : red, 'yellow': yellow, 'orange': orange }">
      <p v-if="yellow">Sun</p>
      <p v-if="orange">Giant Sun</p>
      <p v-if="red">Red Giant</p>
    </div>
    <div class="top-left d-flex align-items-center">
        <input v-model="inputValue" @change="setColor();changeColors();" id="inputRange" type="range" min="1" max="3" step="1">
        <label class="ms-2" for="inputValue">{{ inputValue }}</label>
      </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      inputValue: 0,
      red: false,
      yellow: true,
      orange: false,
    };
  },
  methods: {
    changeColors(){
      if (this.colorCode === 3){
        this.red = true;
        this.orange = false;
        this.yellow = false;
        console.log(this.red,'red');
      } else if (this.colorCode === 2){
        this.orange = true;
        this.red = false;
        this.yellow = false;
        console.log(this.orange,'orange');
      } else {
        this.yellow = true;
        this.orange = false;
        this.red = false;
        console.log(this.yellow,'yellow');
      }
    },
    setColor(){
      this.colorCode = parseInt(this.inputValue);
      console.log(typeof this.colorCode, this.colorCode);
    },
  },
}
</script>

<style>
@import url('https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css');
* {
  box-sizing: border-box;
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
  background: yellow;
  margin: 50vh auto;
  transition: all 0.3s ease-in-out;
}

.red {
  background: red;
  transform: scale(3);
}

.orange {
  background: orange;
  transform: scale(1.5);
}

.yellow {
  background: yellow;
}
</style>
