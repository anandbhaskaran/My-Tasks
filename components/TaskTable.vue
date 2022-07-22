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
                <th scope="col" class="relative py-3.5 pl-3 pr-4 sm:pr-6">
                  <span class="sr-only">Edit</span>
                </th>
              </tr>
              </thead>
              <tbody class="divide-y divide-gray-200 bg-white">
              <tr v-for="person in people" :key="person.email" :class="[person.completed && 'bg-grey-50']">
                <td class="relative w-12 px-6 sm:w-16 sm:px-8">
                  <input v-model="person.completed" type="checkbox" :value="person.email" class="absolute left-4 top-1/2 -mt-2 h-4 w-4 rounded border-gray-300 text-indigo-300 focus:text-indigo-500 focus:ring-indigo-500 sm:left-6"  />
                </td>
                <td :class="['whitespace-nowrap py-4 pr-3 text-sm font-medium', selectedPeople.includes(person.email) ? 'text-indigo-600' : 'text-gray-900']">
                  {{ person.name }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ person.title }}
                </td>
                <td class="whitespace-nowrap px-3 py-4 text-sm text-gray-500">
                  {{ person.email }}
                </td>
                <td class="whitespace-nowrap py-4 pl-3 pr-4 text-right text-sm font-medium sm:pr-6">
                  <a href="#" class="text-indigo-600 hover:text-indigo-900"
                  >Edit<span class="sr-only">, {{ person.name }}</span></a
                  >
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

<script setup>
import { ref, computed } from 'vue'

const people = ref([
  {
    name: 'Lindsay Walton',
    title: 'Front-end Developer',
    email: 'lindsay.walton@example.com',
    completed: true
  },
  // More people...
])

const selectedPeople = ref([])
const checked = ref(false)
</script>
© 2022 Tailwind Labs Inc. All rights reserved.

Privacy policy
Changelog
