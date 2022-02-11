<template>
  <div style="max-width: 100%; height:auto;">
    <v-list class="white">
      <v-list-item
        class="grey--text text--darken-3 item-calendar text-h6 font-weight-bold list-item-cardlendar"
        v-for="item in items"
        :key="item"
      >
        <ItemCarlendar :item="item" :doctors="doctors" :doctor_id="doctor_id"/>
      </v-list-item>
    </v-list>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, useFetch } from "@nuxtjs/composition-api";
import ItemCarlendar from '~/components/ItemCarlendar.vue';
import axios from 'axios';
export default defineComponent({
  components: { ItemCarlendar },
  setup() {
    const items = ref([6,7,8,9,10,11,12,13,14,15,16,17,18,19,20]);
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
    return { doctors, doctor_id,items};
  }
});
</script>

<style lang="scss" scoped>
.list-item-cardlendar{
  height: 150px;
}
</style>