<script setup>
import { ref } from "vue";

const count = ref(0);
const step = ref(1);
const max = 100;
const history = ref([])

function saveHistory(){
  history.value.push(count.value)
}

function increment() {
  saveHistory()
  if (count.value + step.value > max) {
    console.log("limit!");
    count.value = max;
  } else {
    count.value += step.value;
  }
  console.log(history.value);
}

function decrement() {
  saveHistory()
  if (count.value - step.value < 0) {
    console.log("limit!");
    count.value = 0;
  } else {
    count.value -= step.value;
  }
}

function reset() {
  if (count.value === 0){
    count.value = 0;
  }
  else{
    saveHistory()
    count.value = 0;
  }
}

function undo() {
  if(history.value.length === 0){
    console.log("nothing to undo")
    count.value = 0
  }
  else{
  count.value = history.value.pop()
  }
}
</script>

<template>
  <main>
    <div>
      <h1>Counter App</h1>
      <p>Click buttons to change the number.</p>
    </div>

    <div class="count">{{ count }}</div>

    <div class="row">
      <button class="btn inc" @click="increment">Increase</button>
      <button class="btn dec" @click="decrement">Decrease</button>
    </div>

    <div class="row">
      <button class="btn reset" @click="reset">Reset</button>
      <button class="btn undo" @click="undo">Undo</button>
    </div>

    <div class="hint">
      Step : <input type="number" min="1" v-model.number="step" />
    </div>

  </main>
</template>


<style scoped>
  main{
  background-color: rgb(255, 255, 255);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  max-width: 400px;
  padding: 32px;
  gap: 1rem;
  border-radius: 80px;
  text-align: center;
  font-family: Georgia, 'Times New Roman', Times, serif;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);

}
h1{
  font-size: 40px;
  font-weight: 700;
}
.row{
  display: flex;
  justify-content: center;
  width: 100%;
  gap: 1rem;
}
.btn{
  padding: 16px;
  width: 100%;
  max-width: 100px;
  border-radius: 30px;
  background: linear-gradient(to left , rgb(132, 132, 132) , rgb(97, 97, 97));
  cursor: pointer;
  color: white;
  border: none;
  transition: 0.7s;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
  font-size: 12px;
}
.btn:hover{
  transition: 0.7s;
  scale: 1.05;
  opacity: 0.9;
}
.inc{
  background: linear-gradient(to right, rgb(52, 199, 3) , rgb(78, 205, 5));
}
.dec{
  background: linear-gradient(to right, rgb(218, 15, 4) , rgb(246, 78, 52));
}
.count{
  font-size: 50px;
}
.hint input{
  padding: 8px;
  max-width: 64px;
  border-radius: 16px;
  border: none;
  background-color: rgb(235, 235, 235);
  outline: none;
}

</style>