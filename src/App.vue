<template>
  <div class="">
    <h3 class=" text-center bg-primary text-white p-3">Todo Test With Vue</h3>

    <div class="container">
      <div class="row">
        <div class="col mb-4">Task</div>
        <div class="col-2 mb-4">Done</div>
      </div>
      <!-- v-bind:key or :key -->
      <div class="row" v-for="(task,index) in filterTask" v-bind:key="index">
        
        <!--:class="task.done ? 'taskdone' : '' " or OUT KA HRR LO  -->
        <div class="col" :class="{'taskdone' : task.done}" >{{ task.action }}</div>
        <div class="col-2">
          <input type="checkbox" v-model="task.done"/>
        </div>
      </div>

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
      tasks : [
        {
          action : 'task1',
          done : true
        },
        {
          action : 'task2',
          done : false
        },
        {
          action : 'task3',
          done : true
        },
        {
          action : 'task4',
          done : true
        },
      ]
    }),

    // computed so return pyan ma mal
    computed : {
      filterTask(){
        return this.hideComplete ? this.tasks.filter(v => !v.done) : this.tasks
      }
    },

    //method so yin return pyan sa yrr ma lo
    methods : {
      filterMethod(){

      }
    }
  }
</script>

<style>
  .taskdone{
    text-decoration: line-through;
  }
</style>
