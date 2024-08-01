<template>
    <ul v-if="completedTasks.length > 0">
    <li v-for="item in completedTasks" :key="item.id" >
      <span>
        <input
          type="checkbox"
          :checked="item.status === listStatus"
          @change="() => changeTaskStatus(item.id)"
        />
        <s v-if="listStatus==='COMPLETED'">{{item.title}}</s>
        <span v-else>{{item.title}} </span>
    </span>
    <div>
        <button  @click="deleteTask(item.id)"><i class="fas fa-trash"></i></button>
    </div>
    </li>  
  </ul>
  <div v-else> {{ message }} </div>
</template>
<script setup>
    defineProps(['completedTasks' ,'changeTaskStatus', 'listStatus','message', 'deleteTask'])
</script>