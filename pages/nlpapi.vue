<template>
    <section class = "container">
        <h1>{{title}}</h1>
        <p>{{message}}</p>
        <div>
            <textarea class= "input" v-model="posting_text"></textarea>
            <button @click="getData">POST</button>
        </div>
        <hr>
            <!-- <h3>Key</h3>
            <input v-model="api_key">
        <hr> -->
        <tr>
            <th>detected text</th>
            <th>sentiment magnitude</th>
            <th>sentiment score</th>
        </tr>
        <tr v-for="data in this.json_data.sentences">
            <td>{{data.text.content}}</td>
            <td>{{data.sentiment.magnitude}}</td>
            <td>{{data.sentiment.score}}</td>
        </tr>
        <hr>
        <button @click="showData">check all response</button>
        <ul>
            <li v-if="showflag">{{json_data}}</li>
        </ul>
        <br>
        <router-link to="/" >HOME</router-link>
    </section>
</template>

<script>
const axios = require('axios');

// Cloud Natural Language API
let url_base = 'https://language.googleapis.com/'
let url_param = 'v1/documents:analyzeSentiment?key='

export default {
    data: function(){
        return{
            title: 'POST form',
            posting_text:'',
            message: 'POST below texts to Google Cloud NLP API (with Vue and axios)',
            json_data:{},
            post_params:{
                "document": {
                    "type": "PLAIN_TEXT",
                    "language": "JA",
                    "content": ""
                },
                "encodingType": "UTF8"
            },
            showflag:false,
            api_key:""
        };
    },
    methods:{
        getData: function() {
            this.api_key = process.env.API_KEY;
            let id_url = url_base + url_param + this.api_key;
            this.post_params.document.content = this.posting_text;
            axios.post(id_url,this.post_params
            ).then(
                (result) => {
                this.message = 'POSTED';
                this.json_data = result.data
            }).catch((error) => {
                // this.message = 'ERROR!';
                this.message = id_url;
                // this.json_data = {};
                this.json_data = id_url;
            });
        },
        showData: function(){
            this.showflag = !this.showflag;
        },
    },
}
</script>

<style>
.input {
    width: 100%; 
    height: 150px;
    padding: 10px 15px; 
    font-size: 16px;
    border-radius: 3px; 
    border: 2px solid #ddd; 
    box-sizing: border-box; 
    overflow-wrap:normal;
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
  color: #345980;
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
