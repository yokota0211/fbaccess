<template>
  <section>
  <h1>{{ title }}</h1>
  <p>{{ message }}</p>
  <input v-model="value">
  <button @click="getData">Click</button>
  <hr>
  <ul v-for="(data, key) in json_data" :key="key">
    <li>
      {{ data.name }} ({{ data.tel }}) [{{ key }}]
    </li>
  </ul>
</section>

</template>

<script>
const axios = require('axios');

//let url = "https://test1226-5d13e-default-rtdb.firebaseio.com/employee.json?orderBy=%22$key%22&equalTo=%22";
//let url = "https://test1226-5d13e-default-rtdb.firebaseio.com/employee.json";

//let url = "https://test1226-5d13e-default-rtdb.firebaseio.com/employee.json?orderBy=";

//https://test1226-5d13e-default-rtdb.firebaseio.com/employee.json?print=pretty
//参考：https://firebase.google.com/docs/database/rest/retrieve-data?hl=ja

// https://testfirebase-a7a2e-default-rtdb.firebaseio.com/student.json?orderBy=key&equalTo=0001

export default {
  data() {
    return {
      title:'Axios',
      message:'axios sample.',
      json_data: {},
      value: '',
    };
  },
  methods: {
    getData() {
      const url = 'https://testfirebase-a7a2e-default-rtdb.firebaseio.com/student.json';
      axios.get(url, {
        params: {
        orderBy: `"$key"`,
        equalTo: `"${this.value}"`,
        }
      }).then(res => {
        this.message = `get ID=${this.value}`;
        this.json_data = res.data;
        console.log(res);
      }).catch(error => {
        this.message = 'EROR!';
        console.error(error);
      });
    },
  },
}
</script>
