<template>
  <v-app>
    <NavBar :doctors="doctors" :doctor_id="doctor_id"/>
    <v-main class="white black--text">
      <v-container fluid>
        <router-view>
          <Nuxt/>
        </router-view>
      </v-container>
    </v-main>

    <v-footer elevation="10"  app class="grey lighten-3 footer">
       <v-container>
          <Footer/>
        </v-container>
     
    </v-footer>
  </v-app>
</template>

<script lang="ts">
import { defineComponent, ref, useFetch } from "@nuxtjs/composition-api";
import axios from "axios";

export default defineComponent({
  setup() {
    const doctor_id = new URL(location.href).searchParams.get('doctor_id');
    const doctors = ref(null);
    if (localStorage.getItem("doctors")) {
      doctors.value = JSON.parse(localStorage.getItem("doctors") as string);
      
    } else {
      useFetch(async () => {
        doctors.value = await axios
          .get(
            "https://my-json-server.typicode.com/pqcuong737/jsonfakeserver/data"
          )
          .then((res) => {
            localStorage.setItem("doctors", JSON.stringify(res.data));
            return res.data;
          });
      });
    }
    return {doctors, doctor_id};
  }
});
</script>

<style lang="scss" scoped>
</style>