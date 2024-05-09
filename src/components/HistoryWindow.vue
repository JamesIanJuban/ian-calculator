<template>
    <transition name="slide-fade">
      <div v-if="show" class="absolute top-0 left-0 w-full h-full flex justify-center items-center z-50 bg-black bg-opacity-50">
        <div class="bg-white rounded-lg p-8 max-w-lg">
          <h3 class="text-lg font-semibold mb-4">History</h3>
          <ul class="divide-y divide-gray-300">
            <li v-for="(calculation, index) in history.slice().reverse()" :key="index" class="py-2">{{ calculation }}</li>
          </ul>
          <button @click="toggle" class="mt-4 bg-red-500 hover:bg-red-600 text-white font-semibold px-4 py-2 rounded-lg focus:outline-none">Close</button>
        </div>
      </div>
    </transition>
  </template>
  
  <script>
  export default {
    props: {
      show: Boolean,
      history: Array
    },
    methods: {
      toggle() {
        this.$emit('toggle');
      }
    }
  };
  </script>