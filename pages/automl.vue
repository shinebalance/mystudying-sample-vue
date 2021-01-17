<template>
    <section class = "container">
        <h1>{{title}}</h1>
        <p>{{message}}</p>
        <div>
            <input class= "input" v-model="find">
            <button @click="getData">Click</button>
        </div>
        <hr>
            <h3>Token</h3>
            <input v-model="api_token">
        <hr>
        <ul>
            <li>{{json_data}}</li>
        </ul>
    </section>
</template>

<script>
const axios = require('axios');

// Cloud Natural Language API
let url_base = 'https://automl.googleapis.com/v1/projects/'
let url_param = '407822501479/locations/us-central1/models/TCN62850283666931712:predict'
let access_token = ''

export default {
    data: function(){
        return{
            title: 'Text posting to Auto ML',
            find:'',
            api_token:'',
            message: 'access Google AutoML Natural Language API',
            json_data:{},
            request:{
                "payload": {
                    "textSnippet": {
                    "content": "",
                    "mime_type": "text/plain"
                    }
                }
            },
            headers:{
                "Authorization": '',
                "Content-Type": "application/json",
            },
        };
    },
    methods:{
        getData: function() {
            let id_url = url_base + url_param;
            // 入力値をもとにヘッダーとPOSTするJSONを更新
            this.request.payload.content = this.find;
            // this.headers.Authorization = "Bearer " + this.api_token;
            this.headers.Authorization = 'Bearer '+ access_token
            // POST処理
            axios.post(id_url,this.request//,this.headers
            ).then(
                (result) => {
                this.message = 'POSTED';
                this.json_data = result.data
            }).catch((error) => {
                this.message = 'ERROR!';
                this.json_data = {};
                // this.json_data = ${API_TOKEN};
            });
        },
    },
}
</script>

<style>
.input {
    width: 100%; /*親要素いっぱい広げる*/
    padding: 10px 15px; /*ボックスを大きくする*/
    font-size: 16px;
    border-radius: 3px; /*ボックス角の丸み*/
    border: 2px solid #ddd; /*枠線*/
    box-sizing: border-box; /*横幅の解釈をpadding, borderまでとする*/
}
tr th {
    width:150px;
    background-color: darkblue;
    color:white;
    font-size:16pt;
}
tr td {
    padding:5px 10px;
    background-color:#eef;
    font-size:14pt;
}
.container {
  padding: 5px 10px;
}
h1 {
  font-size: 60pt;
  color: #a5eb6c;
}
p {
  padding-top:5px;
  font-size: 20pt;
}
div {
    font-size:20pt;
}
pre {
  padding: 10px;
  font-size: 18pt;
  background-color: #efefef;
  white-space: pre-wrap ;
}
hr {
  margin:10px 0px;
}
ul {
    margin:0px 10px;
    background-color: aliceblue;
}
li {
  padding: 10px;
  font-size: 16pt;
}
</style>
