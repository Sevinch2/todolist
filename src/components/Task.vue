<template>
    <div class="container">
      <div class="task">
        <!-- title -->
        <div class="title">
          <h1>To Do List</h1>
        </div>
        <!-- form -->
        <div class="form">
          <input 
          type="text" 
          placeholder="New Task" 
          v-model="newTask" 
          @keyup.enter="addTask"/>
          <button @click="addTask"><i class="fas fa-plus"> 
            <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960" width="24px" fill="#5f6368"><path d="M440-440H200v-80h240v-240h80v240h240v80H520v240h-80v-240Z"/></svg>
        </i></button>
        </div>
        <!-- task lists -->
        <div class="taskItems">
          <ul>
            <task-item 
            v-bind:task="task" 
            v-for="(task, index) in tasks"
            :key="task.id" 
            @remove="removeTask(index)"
            @complete="completeTask(task)"
            ></task-item>
          </ul>
        </div>
        <!-- buttons -->
        <div class="clearBtns">
          <button @click="clearCompleted">Clear completed</button>
          <button @click="clearAll">Clear all</button>
        </div>
        <!-- pending task -->
        <div class="pendingTasks">
          <span>Pending Tasks: {{ incomplete }}</span>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import TaskItem from './Task-item.vue';

  export default {
    name: "Task",
    props: ['tasks'],
    components: {
        TaskItem
    },
    data(){
        return{
            newTask: "",
        }
    },
    computed: {
        incomplete(){
            return this.tasks.filter(this.inProgress).length;
        }
    },
    methods:{
        addTask() {
            if(this.newTask) {
                this.tasks.push({
                    title: this.newTask,
                    completed: false
                });
                this.newTask = ""
            }
        },
        inProgress(task){
            return !this.isCompleted(task);
        },
        isCompleted(task){
            return task.completed;
        },
        clearCompleted() {
            this.tasks = this.tasks.filter(this.inProgress);
        },
        clearAll(){
            this.tasks = [];
        },
        removeTask(index){
            this.tasks.splice(index, 1);
        },
        completeTask(task){
            task.completed = !task.completed;
        }
    },
  };
  </script>
  <style>
input{
    width: 100%;
    height: 50px;
    font: 15px /1.4 Poppins, sans-serif;
    padding: 15px;
    background: #f3f3f3;
    color: #333;
    border: 1px solid transparent;
    border-radius: 10px;
    transition: border .3s linear;
}
</style>
 