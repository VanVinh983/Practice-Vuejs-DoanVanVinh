<template>
  <nav>
    <v-toolbar elevation="2" dense max-width="100%" flat app class="cyan">
      <v-icon left color="white">mdi-menu</v-icon>
      <v-toolbar-title class="white--text">
        <span class="font-weight-bold headline"> {{textDate}} </span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn flat class="transparent">
        <span class="text-capitalize">SignOut</span>
        <v-icon right color="white">mdi-exit-to-app</v-icon>
      </v-btn>
    </v-toolbar>
  </nav>
</template>
<script lang="ts">
import { defineComponent, ref } from "@nuxtjs/composition-api";

export default defineComponent({
  props: {
    doctor_id: [String],
    doctors: {
      type: [Array, Object],
      default: function () {
        return [];
      },
    },
  },
  setup(props: any){
    const doctor = ref();
    if (props.doctors) {
      props.doctors.forEach((d:any) => {
        if (Number(props.doctor_id) === d.doctor_id) {
          doctor.value = d;
        }
      });
    }
    const textDate = 'Lịch khám bệnh ngày '+ new Date().toLocaleTimeString()+' - Bác sĩ: '+ doctor.value.doctor_name;
    return{textDate};
  }
});
</script>

<style lang="scss" scoped>
</style>