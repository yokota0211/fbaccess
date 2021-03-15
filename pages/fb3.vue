<template>
  <section>
    <h1>{{ title }}</h1>
    <p>{{ message }}</p>
    <div>
      <input type="number" v-model="range.startAt" />
      <span>〜</span>
      <input type="number" v-model="range.endAt" />
    </div>
    {{ value }}
    <button @click="getData">Click</button>
    <hr>
    <ul v-for="(data, key) in json_data" :key="key">
      <li>
        {{ key }} {{ data }}
      </li>
    </ul>
  </section>
</template>

<script>
const axios = require('axios');

//let url = "https://test1226-5d13e-default-rtdb.firebaseio.com/employee.json?orderBy=%22age%22";
// let url = "https://testfirebase-a7a2e-default-rtdb.firebaseio.com/student.json?orderBy=%22age%22";

export default {
  data() {
    return {
      title:'Axios',
      range: {
        startAt: 0,
        endAt: 0,
      },
      message:'axios sample.',
      json_data:{},
    };
  },
  methods: {
    getData() {
      const baseURL = 'https://testfirebase-a7a2e-default-rtdb.firebaseio.com/student.json';
      axios.get(baseURL, {
        params: {
          orderBy: `"age"`,
          startAt: this.range.startAt,
          endAt: this.range.endAt,
        }})
        .then(res => {
          this.message = `get: ${this.range.startAt} < age < ${this.range.endAt}`;
          this.json_data = res.data;
        })
        .catch(error => {
          this.message = 'ERROR!';
          console.error(error);
          this.json_data = {};
        });
    },
  },
}
</script>
