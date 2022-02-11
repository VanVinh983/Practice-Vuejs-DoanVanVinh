<template>
  <v-layout row>
    <v-flex xs12>
      <v-layout row style="margin: 10px">
        <v-flex xs1 class="column-hours">
          <span v-if="item < 10"> 0{{ item }}:00</span>
          <span v-else> {{ item }}:00 </span>
        </v-flex>
        <v-flex xs11>
          <v-layout row class="list-item">
            <v-flex xs12>
              <v-divider class="grey text--darken-3">inset</v-divider>
            </v-flex>
          </v-layout>
          <v-layout row>
            <v-flex xs12>
              <div class="list-doctor">
                <v-layout row class="contain-item-list">
                  <div
                    class="item-doctor"
                    v-for="(patient, index) in patients"
                    :key="index"
                    id="item-doctor"
                    :style="{
                      'border-left': '10px solid' + patient.color_code,
                    }"
                  >
                    <v-spacer></v-spacer>
                    <v-layout row>
                      <v-avatar v-if="patient.avatar != null">
                        <img
                          class="white"
                          :src="patient.avatar"
                          :alt="patient.requester"
                        />
                      </v-avatar>
                      <v-avatar v-if="patient.avatar == null">
                        <img
                          class="white"
                          src="https://cdn2.iconfinder.com/data/icons/people-flat-design/64/Sick-Fever-Ill-Sickness-Patient-Sweating-Avatar-512.png"
                          :alt="patient.requester"
                        />
                      </v-avatar>
                    </v-layout>
                    <v-layout row>
                      <span class="text-h6"> {{ patient.requester }} </span>
                    </v-layout>
                    <v-layout row>
                      <div v-if="patient.status === 'approved'">
                        <v-icon small color="cyan">mdi-circle-outline</v-icon>
                      </div>
                      <div v-else-if="patient.status === 'pending'">
                        <v-icon small color="red">mdi-circle-outline</v-icon>
                      </div>
                      <div v-else>
                        <v-icon small color="green">mdi-circle-outline</v-icon>
                      </div>
                      <span>{{
                        patient.symptom.substring(0, 20) + "..."
                      }}</span>
                    </v-layout>
                  </div>
                </v-layout>
              </div>
            </v-flex>
          </v-layout>
        </v-flex>
      </v-layout>
    </v-flex>
  </v-layout>
</template>

<script>
import { computed, defineComponent, ref } from "@nuxtjs/composition-api";
import axios from "axios";

export default defineComponent({
  props: {
    item: [Number, String],
    doctor_id: [String],
    doctors: {
      type: [Array, Object],
      default: function () {
        return [];
      },
    },
  },
  setup(props) {
    const doctor = ref(null);
    const patients = ref([]);
    if (props.doctors) {
      props.doctors.forEach((d) => {
        if (Number(props.doctor_id) === d.doctor_id) {
          doctor.value = d;
        }
      });
    }
    const dateCurrent = props.item + ":0:0";
    doctor.value.appoitment_calendar.forEach((a) => {
      const startTime = new Date(a.start_time);
      const strStartTime =
        startTime.getHours() +
        ":" +
        startTime.getMinutes() +
        ":" +
        startTime.getSeconds();
      if (strStartTime === dateCurrent) {
        patients.value.push(a);
      }
    });
    return { doctor, patients };
  },
});
</script>

<style lang="scss" scoped>
.list-item {
  margin-top: 15px;
}
.list-doctor {
  width: 100%;
  height: 150px;
  padding: 10px;
}
.column-hours {
  border-right: 1px solid grey;
  text-align: right;
  padding-right: 15px;
}
.contain-item-list {
  width: 100%;
  height: 100%;
  margin: auto;
  margin-left: 10px;
  margin-right: 10px;
  border-radius: 20px;
  border: 1px solid grey;
  display: flex;
  overflow: hidden;
}
.item-doctor {
  display: inline;
  border-right: none;
  padding: 20px;
  border-top-left-radius: 20px;
  border-bottom-left-radius: 20px;
  border-left: 10px solid red;
  width: 50%;
}
</style>