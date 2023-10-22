<template>
  <div class="container">
    <h2 class="text-center mt-5">My Vue Todo App</h2>

    <!--Inputs-->
    <div class="d-flex">
      <input v-model="task" type="text" class="form-control" placeholder="enter tassk">
      <button @click="submitTask" class="btn btn-warning rounded-0">Submit</button>
    </div>

    <!--Task table-->
    <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">Edit task</th>
      <th scope="col" class="text-center">Delete task</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <td><span :class="{'finished': task.status === 'finished'}">{{ task.name }}</span></td>
      <td style="width: 120px;"><span @click="changeStatus(index)" class="pointer" :class="{'text-danger': task.status === 'to-do','text-warning': task.status === 'in-progress','text-success': task.status === 'finished'}">{{ task.status }}</span></td>
      <td>
        <div class="text-center" @click="editTask(index)">
          <span class="fa fa-pen"></span>
        </div>
      </td>
      <td>
        <div class="text-center" @click="deleteTask(index)">
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
    name: 'ToDOApp',
    data() {
      return {
        task : '',
        editedTask : null,
        availableStatuses : ['to-do', 'in-progress', 'finished'],
        tasks: [
          {
            name: 'do your mom',
            status: 'to-do',
          },
          {
            name: 'doing your mom',
            status: 'in-progress',
          },
        ]
      }
    },
    methods: {
      submitTask() {
        if(this.task.length === 0) return;

        if(this.editedTask === null){
        this.tasks.push({
          name: this.task,
          status:'to-do '
        });
      }else{
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }
        this.task = '';
      },
      deleteTask(index) {
        this.tasks.splice(index, 1);
      },
      editTask(index) {
        this.task = this.tasks[index].name;
        this.editTask = index;
      },
      changeStatus(index) {
        let newIndex = this.availableStatuses.indexOf(this.tasks[index].status)
        if(++newIndex > 2) newIndex = 0;
        this.tasks[index].status = this.availableStatuses[newIndex];
      }
    }
  }
</script>

<style>
  .poimter {
    cursor: pointer;
  }

  .finished{
    text-decoration: line-through;
  }
</style>