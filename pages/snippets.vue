<template>
    <section class = "container">
        <h1>{{title}}</h1>
        <p>{{message}}</p>
        <hr>
        <h2>"v-for"</h2>
        <ul v-for="link in this.page_links">
              <li>{{link.name}}</li>
        </ul>
        <br>
        <router-link to="/" >HOME</router-link>
    </section>
</template>


<script>

export default {
    data: function(){
        return{
            title: 'my tips',
            find:'',
            message: '',
            page_links:[
              {"name": "POSTING Cloud NLP","link":"nlpapi"},
              {"name": "AUTOML","link":"automl"},
              {"name": "HOME","link":"/"},
            ],
        };
    },
}
</script>

<style>
.container {
  padding: 5px 10px;
}
h1 {
  font-size: 60pt;
  color: #658034;
}
p {
  padding-top:5px;
  font-size: 20pt;
}
hr {
  margin:10px 0px;
}
ul {
    margin:0px 10px;
    background-color: rgb(240, 255, 242);
}
li {
  padding: 10px;
  font-size: 16pt;
}
</style>
