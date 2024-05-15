<script setup lang="ts">
import { ref } from "vue";

type Task = {
  id: number;
  title: string;
  description: string;
};

const inputTitle = ref<HTMLInputElement>();
const tasks = ref<Task[]>([]);

const newTask = ref<Task>({
  id: 0,
  title: "",
  description: "",
});

function addTask(e: Event) {
  tasks.value.push({
    id: tasks.value.length + 1,
    title: newTask.value.title,
    description: newTask.value.description,
  });

  newTask.value = {
    id: 0,
    title: "",
    description: "",
  };

  inputTitle.value?.focus();
}
</script>

<template>
  <div>
    <h1>To Do</h1>

    <form @submit.prevent="addTask">
      <div>
        <label for="task-title">Title</label>
        <input
          ref="inputTitle"
          type="text"
          name="task-title"
          id="task-title"
          v-model="newTask.title"
        />
      </div>

      <div>
        <label for="task-description">Description</label>
        <input
          type="textarea"
          name="task-description"
          id="task-description"
          v-model="newTask.description"
        />
      </div>

      <div>
        <button type="submit">Add</button>
      </div>
    </form>

    <section>
      <div v-for="task in tasks" :key="task.id">
        <p>{{ task.id }} {{ task.title }} {{ task.description }}</p>
      </div>
    </section>
  </div>
</template>
