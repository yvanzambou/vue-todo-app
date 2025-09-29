<script setup>
  import { ref } from "vue";

  const newTask = ref("");
  const tasks = ref([]);

  function addTask() {
    if (newTask.value.trim() !== "") {
      tasks.value.push({
        text: newTask.value,
        done: false
      });
      newTask.value = "";
    }
  }

  function removeTask(index) {
    tasks.value.splice(index, 1);
  }

  function toggleTask(index) {
    tasks.value[index].done = !tasks.value[index].done;
  }
</script>

<template>
  <div class="min-h-screen bg-gray-100 flex items-center justify-center p-6">
    <div class="bg-white rounded-2x1 shadow-lg w-full max-w-md p-6">
      <h1 class="text-2x1 font-bold mb-4 text-center">Meine Todo-Liste</h1>

      <!-- Eingabe -->
      <div class="flex gap-2 mb4">
        <input
          v-model="newTask"
          @keyup.enter="addTask"
          type="text"
          placeholder="Neue Aufgabe eingeben..."
          class="flex-1 border rounded-x1 px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500"
        />
        <button
          @click="addTask"
          class="bg-blue-500 text-white px-4 py-2 rounded-x1 hover:bg-blue-600">➕</button>
      </div>

      <!-- Aufgabenliste -->
      <ul class="space-y-2">
        <li
          v-for="(task, index) in tasks" :key="index"
          class="flex justify-between items-center bg-gray-200 px-4 py-2 rounded-x1 mt-2"
        >
          <span
            :class="{'line-througth text-gray-400': task.done}"
            @click="toggleTask(index)"
            class="curser-pointer"
          >
            {{ task.text }}
          </span>
          <button
            @click="removeTask(index)"
            class="text-red-500 hover:text-red-700"
          >
            ✖
          </button>
        </li>
      </ul>

      <!-- Keine Aufgabe -->
      <p
        v-if="tasks.length === 0"
        class="text-center text-gray-400 mt-4"
      >
        Keine Aufgaben
    </p>
    </div>
  </div>
</template>

<style scoped></style>c