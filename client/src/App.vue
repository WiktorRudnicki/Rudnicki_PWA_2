<template>
  <div id="app" class="container d-flex flex-column justify-content-center align-items-center mt-5">
    <h3>Willkommen bei der Service Worker Untersuchung!</h3>
    <ButtonGet @get="fetchData"></ButtonGet>
    <CardView :employees="employees" @del="delEmployee"></CardView>
  </div>
</template>

<script>
import ButtonGet from '@/components/ButtonGet.vue';
import CardView from '@/components/CardView.vue';
import axios from 'axios';
import dotenv from 'dotenv';

export default {
  name: 'app',
  components: {
    ButtonGet,
    CardView,
  },
  data() {
    return {
      employees: [],
      serverAddress: process.env.VUE_APP_SERVER,
    };
  },
  methods: {
    async fetchData() {
      console.log('fetchData called');
      let call = await axios({"url": "http://localhost:3000/employees", "method":"get"});
      this.employees = call.data;

    },
    async delEmployee(ob) {
      console.log(ob.id);
      await axios({"url": "http://localhost:3000/employees/"+ ob.id, "method":"delete"});
      this.fetchData();

    },
    updateAvailable() {
      alert("There is an update available, please restart the app!")
    }
  },
  created () {
    dotenv.config();
    document.addEventListener('swUpdated', this.updateAvailable, { once: true });
  }
};
</script>

<style></style>
