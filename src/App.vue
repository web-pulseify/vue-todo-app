<script setup>
import { ref,computed } from "vue";
const tasks = ref(
[
  {
    "id": 1,
    "title": "Tidy Up the House",
    "status": "ACTIVE"
  },
  {
    "id": 2,
    "title": "Reach Out to Family",
    "status": "ACTIVE"
  },
  {
    "id": 3,
    "title": "Go Shopping",
    "status": "ACTIVE"
  },
  {
    "id": 4,
    "title": "Spend an Hour Reading 'Atomic Habits'",
    "status": "COMPLETED"
  }
]
);

const newItemTitle = ref('');

const activeTasks = computed(()=> tasks.value.filter(el => el.status ==='ACTIVE'));
const completedTasks = computed(() => tasks.value.filter(el => el.status ==='COMPLETED'));

function changeTaskStatus(id){
  tasks.value.filter(el => el.id == id)[0].status ='COMPLETED';
}

function deleteTask(id){
  tasks.value.filter(el => el.id == id)[0].status ='DELETED';
}

function addTask(){
 
  tasks.value.push({
    id: tasks.value.length + 1, //if we have 4 item, id must be 5
    title:newItemTitle.value,
    status:'ACTIVE'
  });
   newItemTitle.value = '';
}
</script>

<template>
  <header>
  <h1 >Todo Application</h1>
  <div>
    <input type="text" v-model="newItemTitle"  />
    <button  @click="addTask()">Create</button>
  </div>
</header>
  <main>
    <ul v-if="activeTasks.length > 0">
      <li v-for="item in activeTasks" >
        <span>{{item.title}}</span>
        <div>
          <button  @click="changeTaskStatus(item.id)"><i class="fas fa-check"></i></button>
          <button  @click="deleteTask(item.id)"><i class="fas fa-trash"></i></button>
        </div>
      </li>  
    </ul>
    <div v-else> All Tasks are completed gracefully! </div>
    <ul>
      <li v-for="item in completedTasks" >
        <span><s>{{item.title}}</s></span>
      </li>  
    </ul>
  </main>
</template>
