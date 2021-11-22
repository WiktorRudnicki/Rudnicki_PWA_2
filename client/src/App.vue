<template>
  <div id="app" class="container d-flex flex-column justify-content-center align-items-center mt-5">
    <ButtonGet @get="fetchData"></ButtonGet>
    <CardView :employees="employees" @del="delEmployee"></CardView>
  </div>
</template>

<script>
import ButtonGet from '@/components/ButtonGet.vue';
import CardView from '@/components/CardView.vue';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    ButtonGet,
    CardView,
  },
  data() {
    return {
      employees: [],
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
  },
};
</script>

<style></style>
