<script setup>
import { ref,computed } from "vue";
import List from "./List.vue";
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

function changeTaskStatus(id) {
  const task = tasks.value.find((el) => el.id === id);
  if (task) {
      task.status = task.status === "ACTIVE" ? "COMPLETED" : "ACTIVE";
  }
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
  <h1 >Just Do It.</h1>
  <div>
    <input type="text" v-model="newItemTitle"  />
    <button @click="addTask()">Create</button>
  </div>
</header>
  <main>
    <List 
      :completed-tasks="activeTasks"
      :change-task-status="changeTaskStatus"
      :list-status="'PENDING'"
      :message = "'All tasks have been completed 🚀'"
      :delete-task="deleteTask"
    />
    <List 
      :completed-tasks="completedTasks"
      :change-task-status="changeTaskStatus"
      :list-status="'COMPLETED'"
      :message = "''"
      :delete-task="deleteTask"
    />
  </main>
</template>
