<template>
  <div class="container">
   <h2 class="text-center">Todo App</h2>
<div class="d-flex">
<input v-model="task" type="text" placeholder="Enter Task here" class="form-control">
<button @click="submitTask" class="btn btn-success rounded-0 ms-2">Submit</button>
</div>
<!--task table-->

<table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col" class="text-center">status</th>
      <th scope="col" class="text-center">update</th>
      <th scope="col" class="text-center">Delete</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <td>
      <span :class="{'finished': task.status === 'finished'}">{{task.name}}</span>
      </td>
      <td style="width:120px"><span @click="changeStatus(index)" class="pointer" :class="{'text-danger': task.status === 'to-do',
      'text-success': task.status === 'finished'}"
      >
      {{firstCharUpper(task.status)}}
      </span></td>
      <td>
          <div class="text-center" @click="editTask(index)">
          <i class="fa-solid fa-pen"></i>
      </div>
      
      </td>
      <td> <div class="text-center" @click="deleteTask(index)"><i class="fa-solid fa-trash"></i>
      </div></td>
    </tr>
   
  </tbody>
</table>


  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
data(){
  return{
    task:'',
    editedTask:null,
    availableStatuses: ['to-do','in-progress','finished'],
    tasks:[
      {
        name:'reading',
        status:'to-do'
      },
      {
        name:'running',
        status:'in-progress'
      }
    ]
  }
},

methods:{
  submitTask(){
  if(this.task.length === 0)return;

  if(this.editedTask === null){

  this.tasks.push({
    name: this.task,
    status:'to-do'
    });
   }else{
    this.tasks[this.editedTask].name = this.task;
    this.editedTask = null;
   }
  this.task = '';
  },
  deleteTask(index){
    this.tasks.splice(index, 1);
  },

  editTask(index){
    this.task = this.tasks[index].name;
    this.editedTask = index
  },

changeStatus(index){
let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
if(++newIndex > 2) newIndex = 0;
this.tasks[index].status = this.availableStatuses[newIndex];
},
firstCharUpper(str){
  return str.charAt(0).toUpperCase() + str.slice(1);
}
 }
};
</script>

<style scoped>
.pointer {
  cursor: pointer;
}
.finished {
text-decoration: line-through;
}
</style>
