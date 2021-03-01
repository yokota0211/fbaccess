<template>
<section>
<table>
    <tr>
     <th>id</th>
     <td><input v-model="id"></td>
    </tr>
    <tr>
     <th>age</th>
     <td><input v-model="age"></td>
    </tr>
    <tr>
     <th>mail</th>
     <td><input v-model="mail"></td>
    </tr>
    <tr>
     <th>name</th>
     <td><input v-model="name"></td>
    </tr>
    <tr>
     <th>tel</th>
     <td><input v-model="tel"></td>
    </tr>
    <tr><th></th></td>
        <button @click="addData">Click</button>
    </td></tr>
</table>
<hr>
<ul v-for="(data, key) in json_data">
 <li><strong>{{key}}</strong><br>{{data}}</li>
</ul>
</section>
</template>

<script>
const axios = require('axios');

let url = "https://test1226-5d13e-default-rtdb.firebaseio.com/employee";

export default {
    data: function(){
        return {
            title:'Axios',
            id:'',
            age:0,
            mail:'',
            name:'',
            tel:'',
            message:'axios sample.',
            json_data:{},
        };
    },
    methods: {
    addData: function() {
        let add_url = url + '/' + this.id + '.json';
        let data = {
            'age':this.age,
            'mail':this.mail,
            'name':this.name,
            'tel':this.tel
        };
        axios.put(add_url, data).then((res) => {
            this.id = '';
            this.age = 0;
            this.mail = '';
            this.name = '';
            this.tel = '';
            this.getData();
        });
    },
    getData: function() {
        axios.get(url + '.json').then((res) => {
            this.message = 'get all data.';
            this.json_data = res.data;
        }).catch((error) =>{
            this.message = 'EROR!';
            this.json_data = {};
        });
    }
    },
    created: function(){
        this.getData();
    }
}
</script>