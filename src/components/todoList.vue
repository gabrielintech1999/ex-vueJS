<template>
  <div id="app">
    <h1>To-Do List</h1>
    <input
      v-model="newTask"
      @keyup.enter="addTask"
      placeholder="Add a new task"
    />
    <ul>
      <li v-for="task in tasks" :key="task.id">
        <input type="checkbox" v-model="task.completed" />
        <span :class="{ completed: task.completed }">{{ task.text }}</span>
        <button @click="editTask(task)">Edit</button>
        <button @click="deleteTask(task.id)">Delete</button>
      </li>
    </ul>
    <div v-if="editMode">
      <input v-model="editTaskText" @keyup.enter="updateTask" />
      <button @click="updateTask">Update</button>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const newTask = ref("");
    const tasks = ref([]);
    const editMode = ref(false);
    const currentTaskId = ref(null);
    const editTaskText = ref("");

    const addTask = () => {
      if (newTask.value.trim()) {
        tasks.value.push({
          id: Date.now(),
          text: newTask.value,
          completed: false,
        });
        newTask.value = "";
      }
    };

    const editTask = (task) => {
      editMode.value = true;
      currentTaskId.value = task.id;
      editTaskText.value = task.text;
    };

    const updateTask = () => {
      const taskIndex = tasks.value.findIndex(
        (task) => task.id === currentTaskId.value
      );
      if (taskIndex !== -1) {
        tasks.value[taskIndex].text = editTaskText.value;
        resetEditMode();
      }
    };

    const deleteTask = (id) => {
      tasks.value = tasks.value.filter((task) => task.id !== id);
    };

    const resetEditMode = () => {
      editMode.value = false;
      currentTaskId.value = null;
      editTaskText.value = "";
    };

    return {
      newTask,
      tasks,
      addTask,
      editTask,
      updateTask,
      deleteTask,
      editMode,
      editTaskText,
    };
  },
};
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>
