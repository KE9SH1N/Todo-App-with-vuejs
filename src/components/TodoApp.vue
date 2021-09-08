<template>
  <div class="container">
    <h2 class="text-center mt-5">My Todo App</h2>
    <!-- input -->
    <div class="d-flex">
      <input v-model="task" type="text" class="form-control" placeholder="Enter Task">
      <button @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
    </div>

    <!-- Task Table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr class="text-center">
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col">Edit</th>
          <th scope="col">Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr class="text-center" v-for="(task, index) in tasks" :key="index">
          <td>
            <span :class="{'finished': task.status === 'finished'}">{{firstCharUpper(task.name)}}</span>
            </td>
          <td>
            <span @click="changeStatus(index)" class="pointer" :class="{'text-success': task.status === 'finished','text-warning': task.status === 'in-progress'}">
              {{firstCharUpper(task.status)}}
              </span>
            </td>
          <td><div class="text-center" @click="editTask(index)">
                <span class="fa fa-pen"></span>
              </div>
          </td>
          <td><div class="text-center" @click="deleteTask(index)">
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
  name: 'HelloWorld',
  props: {
    msg: String
  },


  data(){
    return{
      task: '',
      editedTask: null,
      availableStatuses: ['in-progress', 'finished','done! Delete It Now'],
      tasks:[
        
      ]
    }
  },

  methods: {
    submitTask(){
      if(this.task.length === 0) return;


      if(this.editedTask === null){
        this.tasks.push({
        name: this.task,
        status: 'To-do'
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
      this.editedTask = index;
    },

    changeStatus(index){
    let newIndex =  this.availableStatuses.indexOf(this.tasks[index].status)

    if(++newIndex > 2) newIndex = 2;
    this.tasks[index].status = this.availableStatuses[newIndex];

    },

    firstCharUpper(str){
      return str.charAt(0).toUpperCase() + str.slice(1);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

    .pointer{
      cursor: pointer;
    }

    .finished{
      text-decoration: line-through;
    }

</style>
