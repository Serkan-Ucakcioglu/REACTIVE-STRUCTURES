<script setup lang="ts">
//import
import { ref } from "@vue/runtime-core";
import axios from "axios";
//

const error = ref("");

//data
const data = ref(null) as any;

//Get Data
const fetchData = () => {
  axios("https://jsonplaceholder.typicode.com/users")
    .then((res) => {
      data.value = res.data;
      console.log("data =>", data.value);
    })
    .catch((err) => {
      console.log(err);
      error.value = err;
    });
};
</script>
<template>
  <div class="container">
    <button class="btn" @click.stop="fetchData">Fetch Get Data</button>
    <div v-if="error">{{ error }}</div>
    <!-- data user  -->
    <div v-for="user in data" :key="user.id">
      <span> <strong>Name</strong> : {{ user.name }}</span>
      <!--  -->

      <!-- data adress info  -->
      <div v-for="street in user" :key="street.id">
        <span v-if="street.city"> <strong>City</strong> : {{ street.city }}</span>
        <span v-if="street.suite"> <strong>Suite</strong> : {{ street.suite }}</span>
        <span v-if="street.street"> <strong>Street</strong> : {{ street.street }}</span>

        <!-- street info geo  -->
        <div v-for="geo in street" :key="geo.id">
          <span v-if="geo.lat"><strong>Geo</strong> Lat : {{ geo.lat }}</span>
          <span v-if="geo.lng"> <strong>Geo Lng</strong>: {{ geo.lng }}</span>
        </div>
        <!--  -->

      </div>
      <!-- user phone  -->
      <span v-if="user.phone"><strong>Phone</strong>: {{ user.phone }}</span>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 600px;
  margin: 0px auto;
}
.container .btn {
  padding: 0px 10px;
  height: 35px;
  border-color: #3498db;
  color: #fff;
  box-shadow: 0 0 40px 40px #3498db inset, 0 0 0 0 #3498db;
  transition: all 150ms ease-in-out;
  border-radius: 4px;
}
.btn:hover{
  color: #fff;
    outline: 0;
}
</style>
