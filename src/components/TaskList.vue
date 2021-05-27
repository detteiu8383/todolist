<template>
  <div class="task-lists">
    <div class="task-list-wrapper">
      <h2>🍊未完のタスク🍊</h2>
      <div v-for="task in incompleteTasks" :key="task.name">
        <div class="name">名前: {{ task.name }}</div>
        <input v-model="task.isDone" type="checkbox" />
      </div>
    </div>
    <div class="task-list-wrapper">
      <h2>🎉完了したタスク🎉</h2>
      <div v-for="task in completedTasks" :key="task.name">
        <div class="name">名前: {{ task.name }}</div>
        <input v-model="task.isDone" type="checkbox" />
      </div>
    </div>
  </div>
  <div>
    <label>
      タスクを追加する
      <input v-model="newTaskName" type="text" />
    </label>
    <button @click="addTask">add</button>
  </div>
</template>

<script>
import { computed, ref } from "vue";

export default {
  setup() {
    const tasks = ref([
      { name: "たまごを買う", isDone: false },
      { name: "リンゴを買う", isDone: true },
    ]);
    const newTaskName = ref("");
    const addTask = () => {
      if (newTaskName.value != "") {
        tasks.value.push({
          name: newTaskName.value,
          isDone: false,
        });
        newTaskName.value = "";
      }
    };
    const completedTasks = computed(() => {
      return tasks.value.filter((task) => {
        return task.isDone;
      });
    });
    const incompleteTasks = computed(() => {
      return tasks.value.filter((task) => {
        return !task.isDone;
      });
    });
    return {
      tasks,
      newTaskName,
      addTask,
      completedTasks,
      incompleteTasks,
    };
  },
};
</script>

<style>
.over500 {
  color: red;
}
</style>
