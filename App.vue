<template>
  <div id="app">
  <h3>Here You Can Create, Update, Delete and See List of all Usres.</h3>
  <h4>Enter User name</h4>
    <input type="text" v-model="nameis" v-on:keyup.enter="PostApi()">
        <table>
          <tr>
            <td>Id</td>
            <td>Name</td>
            <td>Update</td>
            <td>Delete</td>
          </tr>
          <tr v-for="todo of todos" v-bind:key="todo.id">
            <td>{{ todo.id }}</td>
            <td><input type="text" v-model="todo.name"/></td>
            <td><button v-on:click="PutApi(todo.id,todo.name)">Update</button></td>
            <td> <button v-on:click="DeleteApi(todo.id)">Delete</button></td>
          </tr>
        </table>
  </div>
</template>

<script>
import axios from "axios";
const baseUrl="http://localhost:3000/info/";
export default {
  name: 'App',
  data(){
    return{
      todos:[]
    }
  },
  methods:{
    async GetApi() {
      await axios
      .get(baseUrl)
      .then(resp=>{
        this.todos = resp.data;
      })
      .catch(err=>{
        console.log(err);
      });
    },
    async PostApi() {
      await axios
      .post(baseUrl,{name:this.nameis})
      .then(resp=>{
        console.log(resp);
        this.nameis='';
        this.GetApi();
      })
      .catch(err=>{
        console.log(err);
      });
    },
    async DeleteApi(id) {
      await axios
      .delete(baseUrl+id)
      .then(resp=>{
        console.log(resp);
        this.GetApi();
      })
      .catch(err=>{
        console.log(err);
      });
    },
    async PutApi(id,name) {
      await axios
      .put(baseUrl+id,{name:name})
      .then(resp=>{
        console.log(resp);
        this.GetApi();
      })
      .catch(err=>{
        console.log(err);
      });
    }
  },
  mounted(){
   this.GetApi();
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-image: url(./assets/ZoomBackgroundv31366x768.jpg);
  background-position: center bottom;
  background-size: cover;
  color: #d8db1f;
  margin-top: 60px;
}
</style>
