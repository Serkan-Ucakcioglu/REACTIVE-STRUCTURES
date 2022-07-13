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
    <button class="btn" @click="fetchData">Fetch Get Data</button>
    <div v-if="error">{{ error }}</div>
    <!-- data user  -->
    <div v-for="user in data" :key="user.id">
      <span> Name : {{ user.name }}</span>
      <!--  -->

      <!-- data adress info  -->
      <div v-for="street in user" :key="street.id">
        <span v-if="street.city"> City : {{ street.city }}</span>
        <span v-if="street.suite"> Suite : {{ street.suite }}</span>
        <span v-if="street.street"> Street : {{ street.street }}</span>

        <!-- street info geo  -->
        <div v-for="geo in street" :key="geo.id">
          <span v-if="geo.lat">Geo Lat : {{ geo.lat }}</span>
          <span v-if="geo.lng"> Geo Lng : {{ geo.lng }}</span>
        </div>
        <!--  -->

      </div>
      <!-- user phone  -->
      <span v-if="user.phone">Phone: {{ user.phone }}</span>
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
}
</style>
