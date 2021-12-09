<template>
 <div class="container">
   <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
   <div v-show="showAddTask">
    <AddTask  @add-task="addTask"/>
   </div>
   
   <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
   
 </div>
   
</template>

<script>
import Header from './components/header.vue'
import Tasks from './components/tasks.vue'
import AddTask from './components/addTask.vue'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks:[],
      showAddTask: false
    }
  },
  methods: {
      toggleAddTask(){
         this.showAddTask = !this.showAddTask
     },
    addTask(task){
      this.tasks =[...this.tasks, task]
    },
    deleteTask(id){
      if(confirm('Are you sure?')){
       this.tasks = this.tasks.filter((task)=>task.id !==id)
      }
    },
    toggleReminder(id){
      this.tasks = this.tasks.map((task)=>task.id ==id ? {...task, reminder :!task.reminder} : task)
     
    }
  },
  created(){
    this.tasks = [
      {
        id:1,
        text:'doctors Appointment',
        day:'March 21st at 2:00pm',
        reminder:true
      },
      {
        id:2,
        text:'Meeting At School',
        day:'November 22nd at 1:30pm',
        reminder:true
      },
       {
        id:3,
        text:'Food Shopping',
        day:'November 22nd at 11:00am',
        reminder:false
      }
    ]
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Open+Sans&display=swap');

  *{
    box-sizing : border-box;
    margin  : 0 ;
    padding : 0 ;
  }

   body{
     font-family : 'Poppins' , sans-serif;
     
   }

   .container{
     max-width : 500px;
     margin: 30px auto;
     overflow: auto;
     min-height: 300px;
     border: 1px solid steelblue;
     padding: 30px;
     border-radius: 30px;
   }
   
   .btn{
     display: inline-block;
     background: #000;
     color: #fff;
     border: none;
     padding: 10px 20px;
     margin: 5px;
     border-radius: 5px;
     cursor: pointer;
     text-decoration: none;
     font-size: 15px;
     font-family: inherit;
   }

   .btn:focus {
      outline: none;
     }
    .btn:active {
      transform: scale(0.98);
     }
    .btn-block {
        display: block;
        width: 100%;
      }
</style>
