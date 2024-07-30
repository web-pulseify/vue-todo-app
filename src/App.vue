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

function changeTaskStatus(id) {
  const task = tasks.value.find((el) => el.id === id);
  if (task) {
    setTimeout(() => {
      task.status = task.status === "ACTIVE" ? "COMPLETED" : "ACTIVE";
    }, 2); // Delay of 1ms
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
    <button   @click="addTask()">Create</button>
  </div>
</header>
  <main>
    <ul v-if="activeTasks.length > 0">
      <li v-for="item in activeTasks"   :key="item.id">
        <div>
          <input
            type="checkbox"
            :checked="item.status === 'COMPLETED'"
            @change="() => changeTaskStatus(item.id)"
          />
          <span>{{item.title}}</span>
        </div>
        
        <div>
          <button  @click="deleteTask(item.id)"><i class="fas fa-trash"></i></button>
        </div>
      </li>  
    </ul>
    <div v-else> All Tasks are completed gracefully! </div>
    <ul v-if="completedTasks.length > 0">
      <li v-for="item in completedTasks" >
        <span>  <input
            type="checkbox"
            :checked="item.status === 'COMPLETED'"
            @change="() => changeTaskStatus(item.id)"
          /><s>{{item.title}}</s></span>
      </li>  
    </ul>
  </main>
</template>
