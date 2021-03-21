<template>
  <section>
    <h1>{{ message }}</h1>
    <form @submit.prevent="addData">
      <table>
        <tr width="300">
          <th>id</th>
          <td colspan="3">
            <input
              type="text"
              v-model="id"
              placeholder="追加/更新したいidを入力"
              required
            >
          </td>
        </tr>
        <tr>
          <th>birthday</th>
          <td>
            <input
              name="年"
              type="number"
              v-model="putData.year"
              placeholder="1990"
              required
            >
          </td>
          <td>
            <input
              type="number"
              v-model="putData.month"
              placeholder="1"
              required
            >
          </td>
          <td>
            <input
              type="number"
              v-model="putData.day"
              placeholder="1"
              required
            >
          </td>
        </tr>
        <tr>
          <th>mail</th>
          <td colspan="3">
            <input type="email" v-model="putData.mail" required>
          </td>
        </tr>
        <tr>
          <th>name</th>
          <td colspan="3">
            <input type="text" v-model="putData.name" required>
          </td>
        </tr>
        <tr>
          <th>tel</th>
          <td colspan="3">
            <input type="tel" v-model="putData.tel" required>
          </td>
        </tr>
        <tr>
          <th></th>
          <td colspan="3">
            <button type="submit">PutData</button>
            <button @click="deleteData">DeleteData</button>
          </td>
        </tr>
      </table>
    </form>

    <hr>

    <table border="1">
      <thead>
        <tr>
          <th>id</th>
          <th>age</th>
          <th>mail</th>
          <th>name</th>
          <th>tel</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(data, key) in json_data" :key="data.key">
          <th>{{ key }}</th>
          <th>{{ birthdayToAge(data.year, data.month, data.day) }}</th>
          <td>{{ data.mail }}</td>
          <td>{{ data.name }}</td>
          <td>{{ data.tel }}</td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      title: 'Axios',
      id: '',
      putData: {
        year: '',
        month: '',
        day: '',
        mail: '',
        name: '',
        tel: '',
      },
      message: 'axios sample.',
      json_data: {},
      baseUrl: 'https://test1226-5d13e-default-rtdb.firebaseio.com/employee',
    };
  },
  methods: {
    putDataInit() {
      const initalData = {
        year: '',
        month: '',
        day: '',
        mail: '',
        name: '',
        tel: '',
      };
      this.putData = {...initalData};
    },
    addData() {
      const url = `${this.baseUrl}/${this.id}.json`;
      const data = this.putData;
      axios.put(url, data)
        .then(res => {
          console.log(res.data);
          this.putDataInit();
          this.getData();
      });
    },
    getData() {
      axios.get(`${this.baseUrl}.json`)
        .then(res => {
          this.message = 'get all data.';
          this.json_data = res.data;
        })
        .catch(error => {
          this.message = 'EROR!';
          console.error(error);
          this.json_data = {};
        });
    },
    birthdayToAge(year, month, day) {
      // 年齢算出ロジック参考
      // https://zenn.dev/awsmgs/articles/96893507976a1f

      const today = new Date();
      const thisYearsBirthday = new Date(today.getFullYear(), month-1, day);
      let age = today.getFullYear() - year;
      if (today < thisYearsBirthday) {
        age = age - 1;
      }
      return age;
    },
    // デバッグ用
    deleteData() {
      const url = `${this.baseUrl}/${this.id}.json`;
      axios.delete(url)
        .then(res => {
          console.log(res.data);
          this.putDataInit();
          this.getData();
      });
    },
  },
  created() {
    this.getData();
  },
}
</script>
<style scoped>
input {
  width: 100%;
}
form table {
  width: 300px;
}
form th {
  text-align: right;
}
</style>
