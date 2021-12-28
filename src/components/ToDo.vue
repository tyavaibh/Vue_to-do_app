<template>
  <div class="container">
    <h1 class="text-center mt-5">'Vue Todo App': CRUD APPLICATION</h1>

    <!-- Input -->
    <div class="d-flex">
      <input type="text" placeholder="enter task..." class="form-control" v-model="inputTask"/>
      <button @click="addTask" class="btn btn-warning rounded-0">Add!</button>
    </div>

    <!-- Task table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">Edit</th>
          <th scope="col" class="text-center">Delete</th>
        </tr>
      </thead>

      <tbody v-for="task,index in tasks" :key="index"> 
        <tr>
          <td scope="row" :class="{finished :task.status=='Finished'}">{{task.name}}</td>

          <td><span @click="changeStatus(index)" class="pointer">{{task.status}}</span></td>
          <td>
              <div class="text-center pointer" @click="updateTask(index)">
                <span class="fa fa-pen"></span>
              </div>
              
          </td>
          <td>
            <div class="text-center pointer" @click="deleteTask(index)" >
                <span class="fa fa-trash"></span>
            </div>
              
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "ToDo",

  data(){
      return {
          tasks:[
              {name:"buy veggies",
              status:'Todo'},
              {name:"Eat 1 kg choclate in an hour",
              status:'In-progress'},
          ],
          inputTask:null,
          editTask:null,
        
      }
  },

  methods:{
      addTask(){
          if(this.inputTask.length===0){
            null
          } 

          if(this.inputTask.length!==0 && this.editTask===null){
            this.tasks.push({name:this.inputTask,status:"Todo"})
            this.inputTask=null;
          }

          if(this.inputTask.length!==0 && this.editTask!==null){
              this.tasks[this.editTask].name=this.inputTask;
              this.inputTask=null;
          }
          
      },

      updateTask(index){
          console.log("Updated");
          this.inputTask=this.tasks[index].name;
          this.editTask=index
      },

      deleteTask(index){
          console.log("Deleted",index);
          this.tasks.splice(index,1)
      },

      changeStatus(index){
          console.log("Change Status",index,this.tasks[index].status);
         if(this.tasks[index].status=='Todo'){
             this.tasks[index].status='In-progress'
         }

         else if(this.tasks[index].status=='In-progress'){
             this.tasks[index].status='Finished'
         }

         else if(this.tasks[index].status=='Finished'){
             this.tasks[index].status='Todo'
         }
      }
  }
};
</script>

<style scoped>
.pointer{
    cursor:pointer;
}

.finished{
    text-decoration: line-through;
}
</style>