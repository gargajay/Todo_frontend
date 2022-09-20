<template>
  <!-- <div class="home min-h-screen">
    <img alt="Vue logo" src="../assets/logo.png">
    
  </div> -->
  


   <!-- component -->
<div class="  w-full flex items-center justify-center min-h-screen  bg-teal-100 font-sans ">
	<div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 ">
        <div class="mb-3">
            <h1 class="text-indigo-600 font-bold font-sans text-4xl text-center">Todo List</h1>
            <div class="flex mt-4">
                <input class="shadow appearance-none border rounded w-full py-2 px-3 mr-4 text-grey-darker"  v-model="todoName" placeholder="Add Todo" />
                <button type="submit" class="flex-no-shrink p-2 border-2 rounded text-teal-600 border-teal hover:text-white hover:bg-teal-500" @click.prevent=" createTodo()">Add</button>
            </div>
        </div>
        <div>
            <div class=" flex mb-5 items-center " v-for="list in todos" :key="list.id">
                <p  v-if="!list.status_id" class="w-full  text-grey-darkest">{{list.name}}</p>
                <p  v-if="list.status_id" class="w-full line-through text-green-600">{{list.name}}</p>
                <button  v-if="list.status_id" class="  flex-no-shrink p-2  ml-4 mr-2 border-2 rounded hover:text-white text-green-600 border-green-500 hover:bg-green-500" @click.prevent="statusUpdate(list.id,0)">Not Done</button>
                <button v-if="!list.status_id" class=" flex-no-shrink p-2 ml-4 mr-2 border-2 rounded  hover:text-white  text-grey-600 border-grey-600 hover:bg-green-500 " @click.prevent="statusUpdate(list.id,1)"> Done</button>

                <button class="flex-no-shrink p-2 ml-2 border-2 rounded text-red-600 border-red-500 hover:text-white hover:bg-red-600" @click.prevent="removeTodo(list.id)">Remove</button>
            </div>
         
        </div>
    </div>
    <HelloWorld msg="Welcome to Your Vue.js App"/>

</div>



  

  <!-- <li v-for="list in todolist" :key="list.id">{{list.name}}</li> -->
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import { constant,config } from './constant'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  },
  created(){
     this.getList()
    //  console.log(this.todolist);
  },
  data(){
        return {
            todoName:'',
            todos:[]
            
        }
      },
  methods:{
    
    getList(){
      const token = localStorage.getItem('token');

      const getConfig ={};

      getConfig.headers = {
              "Content-type":"application/json",
              "Access-Control-Allow-Origin":"*"
          },

          getConfig.method="GET";
          getConfig.headers.Authorization = `Bearer ${token}`;

          

          fetch(constant.BACKEND_URL+'todo/list',getConfig).then(response => {
          if (response.status == 200) {
            return response.json();            
          } else {
            alert(response.statusText);
          }
          }).then(data =>{
                  if(data.data){
                    this.todos = data.data

                    console.log(data.data);
                  }
              });
    },
    createTodo(){
      const token = localStorage.getItem('token');

     
          if(!this.todoName.length){
              alert("Please fill todo name");
          }
         

          config.method="POST";
          config.body=JSON.stringify({name:this.todoName});
          config.headers.Authorization = `Bearer ${token}`;
          fetch(constant.BACKEND_URL+'todo/add',config).then(response => {
          if (response.status == 200) {
            return response.json();            
          } else {
            alert(response.statusText);
          }
          }).then(data =>{
                  if(data.message){
                    this.getList();
                    this.todoName="";
                   alert(data.message);

                   
                  }
              });
          }, 
         
          statusUpdate(id,status) {
            const token = localStorage.getItem('token');

     
            config.method="POST";
            config.body=JSON.stringify({todo_id:id,status_id:status});
            config.headers.Authorization = `Bearer ${token}`;
         
         
          fetch(constant.BACKEND_URL+'todo/status-update',config).then(response => {
          if (response.status == 200) {
            return response.json();            
          } else {
            alert(response.statusText);
          }
          }).then(data =>{
                  if(data.message){
                    this.getList();
                   alert(data.message);

                   
                  }
              });
          },
          removeTodo (id) {

            const token = localStorage.getItem('token');

     
            config.method="POST";
            config.body=JSON.stringify({todo_id:id})
            config.headers.Authorization = `Bearer ${token}`;
         
         
          fetch(constant.BACKEND_URL+'todo/delete',config).then(response => {
          if (response.status == 200) {
            return response.json();            
          } else {
            alert(response.statusText);
          }
          }).then(data =>{
                  if(data.message){
                    this.getList();
                   alert(data.message);

                   
                  }
              });
          },
         
      }


  
}
</script>

<style>


.xHolder {
  padding-top: .4rem;
  color: #EF5753;
  font-size: 2rem;
  transition-duration: .5s;
}

.xHolder i:hover {
  transition-duration: .5s;
  color: red;
  transform: rotate(90deg);
  font-size: 2.5rem;
  cursor: pointer;
}
</style>
