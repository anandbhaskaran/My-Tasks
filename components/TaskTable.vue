<template>
  <div class="px-4 sm:px-6">
    <div class="mt-8 flex flex-col">
      <div class="-my-2 -mx-4 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="inline-block min-w-full py-2 align-middle px-1">
          <div class="relative overflow-hidden shadow ring-1 ring-black ring-opacity-5 md:rounded-lg">
            <table class="min-w-full table-fixed divide-y divide-gray-300">
              <thead class="bg-gray-50">
              <tr>
                <th scope="col" class="relative w-12 px-6 sm:w-16 sm:px-8">

                </th>
                <th scope="col" class="min-w-[12rem] py-3.5 pr-3 text-left text-sm font-semibold text-gray-900">Title</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">Description</th>
                <th scope="col" class="px-3 py-3.5 text-left text-sm font-semibold text-gray-900">Created</th>
              </tr>
              </thead>
              <tbody class="divide-y divide-gray-200 bg-white">
              <tr v-for="task in tasks" :key="task.id" :class="[task.completed && 'bg-grey-50']">
                <td class="relative w-12 px-6 sm:w-16 sm:px-8">
                  <input v-model="task.completed" type="checkbox" class="absolute left-4 top-1/2 -mt-2 h-4 w-4 rounded border-gray-300 text-indigo-300 focus:text-indigo-500 focus:ring-indigo-500 sm:left-6" @change="updateTask(task)"  />
                </td>

                <td :class="['whitespace-nowrap py-4 pr-3 text-sm font-medium', task.completed ? 'text-indigo-600' : 'text-gray-900']">
                  {{ task.title }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ task.description }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ getDate(task.created_at) }}
                </td>
              </tr>
              <tr>
                <td class="relative w-12 px-6 sm:w-16 sm:px-8">
                  <input type="checkbox" disabled class="absolute left-4 top-1/2 -mt-2 h-4 w-4 rounded border-gray-300 text-indigo-300 focus:text-indigo-500 focus:ring-indigo-500 sm:left-6"  />
                </td>
                <td  class="whitespace-nowrap pl-0 pr-3 py-4 text-sm text-gray-500">
                  <input v-model="newTask.title" type="text" class="shadow-sm focus:ring-indigo-500 focus:border-indigo-500 block w-full sm:text-sm border-gray-300 rounded-md" placeholder="Title" />
                </td>
                <td  class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  <input v-model="newTask.description" type="text" class="shadow-sm focus:ring-indigo-500 focus:border-indigo-500 block w-full sm:text-sm border-gray-300 rounded-md" placeholder="Description" />
                </td>
                <td class="whitespace-nowrap px-4 py-4 text-sm text-gray-500">
                  <a href="#" class="text-indigo-600 hover:text-indigo-900" @click="createTask"
                  >Create</a>
                </td>
              </tr>

              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import axios from 'axios';

export default {
  name: 'TaskTable',
  props: {
  },
  setup() {
    const BASE_URI = "https://70nxhlaiqc.execute-api.eu-central-1.amazonaws.com/Live/todo"
    const USER_ID = "1"
    const tasks = ref([]);
    const loading = ref(true);
    const error = ref(null);
    const newTask = ref({
      title: "",
      description: ""
    })
    async function fetchData() {
      loading.value = true;
      const response = await axios.get(BASE_URI + '?user=' + USER_ID)
      tasks.value = response.data.items
    }

    function generateQuickGuid() {
      return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
    }

    async function createTask() {
      await axios.post(BASE_URI, {
        "task_id": generateQuickGuid(),
        "title": newTask.value.title,
        "description": newTask.value.description,
        "completed": "false",
        "user_id": USER_ID,
        "created_at": new Date().toUTCString()
      })
      await fetchData()
    }

    async function updateTask(task) {
      await axios.post(BASE_URI, task)
      await fetchData()
      if(task.completed){
        this.$toast.success('Congrats. You have completed '+ task.title, {
          duration: 1500
        })
      }
    }

    onMounted(() => {
      fetchData();
    });

    function getDate(utcDate){
      const d = new Date(utcDate);
      const month = ["January","February","March","April","May","June","July","August","September","October","November","December"];
      return  d.getDate() + "-" + month[d.getMonth()]
    }

    return {
      tasks,
      loading,
      error,
      newTask,
      createTask,
      updateTask,
      getDate
    };
  }
}
</script>

