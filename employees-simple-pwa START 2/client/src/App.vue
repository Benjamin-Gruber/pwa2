<template>
  <div id="app" class="container d-flex flex-column justify-content-center align-items-center mt-5">
    <ButtonGet @get="fetchData"></ButtonGet>
    <CardView :employees="employees" @del="delEmployee"></CardView>
  </div>
</template>

<script>
import axios from 'axios';
import ButtonGet from '@/components/ButtonGet.vue';
import CardView from '@/components/CardView.vue';

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
      try {
        const { data } = await axios({
          url: 'http://localhost:3000/employees',
          method: 'GET',
        });
        this.employees = data;
      } catch (error) {
        console.error(error);
      }
      console.log('fetchData called');
    },

    async delEmployee(e) {
      try {
        await axios({
          url: `http://localhost:3000/employees/${e.id}`,
          method: 'DELETE',
        });
        this.fetchData();
      } catch (error) {
        console.error(error);
      }
      console.log('delEmployee called');
    },
  },
};
</script>

<style></style>
