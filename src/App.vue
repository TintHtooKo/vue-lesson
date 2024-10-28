<template>
  <div class="">
    <h3 class=" text-center bg-primary text-white p-3">Todo Test With Vue</h3>

    <div class="container">

      <div class="row mt-5">
        <div class="col">
          <input type="text" v-on:keyup.enter="addTask" v-model="newTask" class="form-control">
        </div>
        <div class="col">
          <input type="button" v-on:click="addTask" value="Add" class="btn btn-secondary">
        </div>
        <div class="col">
          <button v-on:click="deleteTask" class="btn btn-danger">Delete</button>
        </div>
      </div>

      <div class="" v-if="filterTask.length > 0">
        <div class="row mt-5">
          <h3 class="col mb-4">Task</h3>
          <h3 class="col-2 mb-4">Done</h3>
        </div>
      <!-- v-bind:key or :key -->
        <div class="row" v-for="(task,index) in filterTask" v-bind:key="index">        
        <!--:class="task.done ? 'taskdone' : '' " or OUT KA HRR LO  -->
          <div class="col" :class="{'taskdone' : task.done}" >{{ task.action }}</div>
          <div class="col-2">
            <input type="checkbox" v-model="task.done"/>
          </div>
      </div>
      </div>

      <div v-else class="alert mt-3 alert-warning text-center">There is no data</div>

      <div class=" bg-danger text-center text-white p-2 mt-5 row">
        <h5 class="col">Hide Completed</h5>
        <input class="col" type="checkbox" v-model="hideComplete"/>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name : 'App',
    data : () =>({
      hideComplete : false,
      newTask : "",
      tasks : []
    }),

    // computed so return pyan ma mal
    computed : {
      filterTask(){
        return this.hideComplete ? this.tasks.filter(v => !v.done) : this.tasks
      }
    },

    //method so yin return pyan sa yrr ma lo
    methods : {
      addTask(){
        if(this.newTask === ""){
          return alert("Please enter a task")
        }
        this.tasks.push({
          action : this.newTask,
          done : false
        })

        this.newTask = ""
        this.storeData()
      },

      deleteTask(){
        this.tasks = this.tasks.filter(v=> !v.done)
        this.storeData()
      },

      storeData(){
        localStorage.setItem('myData',JSON.stringify(this.tasks))
      }
    },

    mounted(){
      let data = localStorage.getItem('myData')
      if(data !== null){
        this.tasks = JSON.parse(data)
      }
    }
  }
</script>

<style>
  .taskdone{
    text-decoration: line-through;
  }
</style>
