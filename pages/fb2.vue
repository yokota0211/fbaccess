<template>
<section>
<h1>{{title}}</h1>
<p>{{message}}</p>
<input v-model="find">
<button @click="getData">Click</button>
<hr>
<ul v-for="(data, key) in json_data">
 <li>{{data.name}} ({{data.tel}}) [{{key}}]</li>
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

let url = "https://testfirebase-a7a2e-default-rtdb.firebaseio.com/student.json?orderBy=%22$key%22&equalTo=%22";

export default {
    data: function(){
        return {
            title:'Axios',
            message:'axios sample.',
            //json_data:{},
        };
    },
    methods: {

 /* 実行時に結果が表示されない...
    getData() {

        const url = "https://testfirebase-a7a2e-default-rtdb.firebaseio.com/student.json";

        axios.get(url, {
         params:{
          orderBy: key,
          equalTo: this.find,
         }   
        }).then((res) => {
            this.message = 'get ID=' + this.find;
            this.json_data = res.data;
            console.log(res);
        }).catch((error) =>{
            this.message = 'EROR!';
           // this.json_data = {};
        });
    },
*/
        getData: function(){

         let r_url = url + this.find + '%22';

         axios.get(r_url).then((res) => {
            this.message = 'get ID=' + this.find;
            this.json_data = res.data;
         }).catch((error) =>{
            this.message = 'EROR!';
            this.json_data = {};
         });
     }


   }
}
</script>