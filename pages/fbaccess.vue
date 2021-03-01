<template>
<section>
<h1>{{title}}</h1>
<p>{{message}}</p>

<!--
 <p>{{json_data}}</p>
-->

<ul v-for="(data, key) in json_data">
 <li>ID:{{key}} 名前:{{data.name}}</li>
</ul>

</section>

</template>

<script>
const axios = require('axios');

//動作確認

let url = "https://testfirebase-a7a2e-default-rtdb.firebaseio.com/student.json"
//let url = ""

export default {
    data: function(){
        return {
            title:'Realtime Database & Axios',
            message:'Nuxt.jsでデータを表示させた！',
        };
    },
    asyncData: async function() {
        let result = await axios.get(url);
        return { json_data: result.data };
    },
}
</script>