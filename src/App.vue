<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <input type="text" v-on:keyup.enter="addTask(task)" placeholder="请添加任务" v-model="task.taskName">
    <ul>
      <li v-for="(task,index) in tasks" v-bind:class="{finshed:task.isFinshed}" v-on:click="toggleFinsh(index)">
        {{ task.taskName }}
      </li>
    </ul>
  </div>
</template>

<script>
import Store from './store'
export default {
  data:function(){
    return {
      title:'任务列表',
      tasks:Store.fetch(),
      task:{taskName:'',isFinshed:false}
    }
  },
  methods:{
    toggleFinsh:function(index){
      this.tasks[index].isFinshed = !this.tasks[index].isFinshed
    },
    addTask:function(task){
      this.tasks.push(task)
      this.task = {taskName:'',isFinshed:false}
    }
  },
  watch:{
    tasks:{
      handler:function(items){
        Store.save(items)
      },
      deep:true
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
ul{
  list-style: none;
}
.finshed{
  color: #673ab7;
}
</style>
