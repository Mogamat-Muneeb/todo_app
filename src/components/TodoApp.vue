<template>
  <div class="container mt-5" >
  <h3>To Do App</h3>
  <div class="mt-5">
    <input v-model="task" type="text" placeholder="Enter to do" class="">
    <button @click="submitTask" class="btn">submit</button>
  </div>
<table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">Edit</th>
      <th scope="col" class="text-center">Delete</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index" >
      <td>{{task.todo}}</td>
      <td> <span class="cursor" @click="statusUpdate(index)">{{task.status}}</span>  </td>
      <td>
         <div class="text-center" @click="updateTask(index)">
           <i class="fas fa-pencil"></i>
         </div>
        </td>
      <td>
        <div class="text-center" @click="deleteTask(index)">
        <i class="fas fa-trash" ></i>
        </div>
      </td>
     </tr>
  </tbody>
</table>
  </div>
</template>

<script>
export default {
  name: 'TodoApp',
  props: {
    msg: String
  },


  data() {
    return {
      task:'',
      updatedTask: null,
      statusType: ['To Do', 'Busy', 'Done'],
      tasks: [
        {
          todo:'Get the task done',
          status:'To Do'
        },
        {
          todo:'Go to the store.',
          status:'Busy'
        }
      ]
    } 
  },
  methods: {
    submitTask(){
       if(this.task.length === 0 ) return;

      if(this.updatedTask === null){
        this.tasks.push({
          todo: this.task,
          status:'To Do'
        });
      }else{
        this.tasks[this.updatedTask].todo = this.task;
        this.updatedTask = null;
      }

       this.task = '';

    }, 

    deleteTask(index){
       this.tasks.splice(index,1);
    },

    updateTask(index){
      this.task = this.tasks[index].todo;
      this.updatedTask =  index; 
    },

    statusUpdate(index){
     let newIndex = this.statusType.indexOf(this.tasks[index].status);
        if(++newIndex > 2) newIndex = 0 ;
        this.tasks[index].status = this.statusType[newIndex];
    },
  }
}
</script>

<style scoped>
 .container {
   text-align: center;
   justify-content: center;
 }

 .cursor{
   cursor: pointer;
 }
</style>
