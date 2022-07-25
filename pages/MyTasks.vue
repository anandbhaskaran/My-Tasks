<template>
  <div class="flex">
  <DarkSidebar current="My Tasks"/>
    <main class="flex-1">
      <div class="py-6">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <h1 class="text-2xl font-semibold text-gray-900">My Tasks</h1>
        </div>
        <div class="max-w-7xl mx-auto px-4 sm:px-6 md:px-8">
          <!-- Replace with your content -->
          <TaskTable/>
          <!-- /End replace -->
        </div>
      </div>
    </main>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
})
</script>
