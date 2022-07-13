<script setup lang="ts">
//import
import { reactive, ref, toRefs, defineProps } from "vue";

//props interfac props type
interface Props {
  message: String;
}
//prosp
const props = defineProps<Props>();

//color bindnig
const color = ref<string | number>();

//my info data type
interface info {
  name: string;
  age: number;
  city: string;
  area: string;
}

const count = ref<number>(0);

//my info
const state: info = reactive({
  name: "Serkan",
  age: 19,
  city: "Ankara",
  area: "Front End Developer",
});

//to seperate
const { name, age, city, area } = toRefs(state);

//max limit 10 count  count >= 0 stop
function countLimit() {
  if (count.value >= 0) {
    if (count.value >= 10) {
      alert("yeter");
    } else {
      count.value++;
    }
  }
}
countLimit();
</script>

<template>
  <!--Props Message -->
  <h1>{{ props.message }}</h1>

  <!-- Count  -->
  <div class="count">
    <button @click="countLimit">+</button>
    <span>{{ count }}</span>
    <button @click="count--">-</button>
  </div>
  <!--  -->

  <!--Color İnput   -->
  <label for="bgColor">Count Background Color</label>
  <input id="bgColor" type="color" v-model="color" />
  <!--  -->

  <!-- My İnfo  -->
  <div class="list">
    <span>Name : {{ name }}</span>
    <span>Age: {{ age }}</span>
    <span>City: {{ city }}</span>
    <span>Area : {{ area }} </span>
  </div>
</template>

<style scoped>
button {
  color: red;
  height: 30px;
  width: 50px;
  background: #f2f2f2;
  font-size: 18px;
  font-weight: bold;
}
#bgColor {
  margin-left: 10px;
}
.list {
  display: flex;
  flex-direction: column;
  height: 300px;
  margin-top: 15px;
}
.list span {
  font-size: 20px;
  font-weight: bold;
}
.count {
  display: flex;
  justify-content: center;
  margin-bottom: 15px;
}
.count span {
  display: flex;
  align-items: center;
  margin: 0px 15px;
  height: 30px;
  padding: 0px 10px;
}

.count button,
.count span {
  border: 1px solid gray;
  background: v-bind(color);
  color: rebeccapurple;
  border-radius: 4px;
  cursor: pointer;
}
</style>
