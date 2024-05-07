<template>
    <div class="container box justify-center items-center p-8 relative">
      <!-- Calculator display -->
    <div class="display mb-6 mt-10 flex justify-center">
      <input type="text" v-model="inputStr" placeholder="Enter Expression" @keydown.enter="calculate" @input="validateInput" class="input-text w-full max-w-xl px-6 py-4 md:py-6 text-lg rounded-lg text-white border-2 border-gray-300 bg-red-600 shadow-lg shadow-red-500/50 dark:shadow-lg dark:shadow-red-800/80 placeholder-gray-100 focus:border-blue-500 focus:outline-none transition duration-300 ease-in-out">
    </div>    
      <!-- Operation buttons -->  
    <div class="grid grid-cols-5 gap-4 px-6 py-4">
      <button v-for="item in numeric" :key="item.text" class="text-white bg-gradient-to-r from-cyan-400 via-cyan-500 to-cyan-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-cyan-300 dark:focus:ring-cyan-800 shadow-lg shadow-cyan-500/50 dark:shadow-lg dark:shadow-cyan-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2" @click="handleButtonClick(item)">{{ item.text }}</button>  
      <button class="text-white bg-gradient-to-r from-red-400 via-red-500 to-red-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-red-300 dark:focus:ring-red-800 shadow-lg shadow-red-500/50 dark:shadow-lg dark:shadow-red-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2 transition duration-300 ease-in-out" @click="remove">←</button>
      <button class="text-white bg-gradient-to-r from-red-400 via-red-500 to-red-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-red-300 dark:focus:ring-red-800 shadow-lg shadow-red-500/50 dark:shadow-lg dark:shadow-red-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2" @click="clear">AC</button>
      <button class="text-white bg-gradient-to-r from-red-400 via-red-500 to-red-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-red-300 dark:focus:ring-red-800 shadow-lg shadow-red-500/50 dark:shadow-lg dark:shadow-red-800/80 font-medium rounded-lg text-sm px-5 py-2.5 text-center me-2 mb-2" @click="calculate">=</button>
    </div>
    <div class="flex justify-center">
      <button class="text-white bg-gradient-to-r from-red-400 via-red-500 to-red-600 hover:bg-gradient-to-br focus:ring-4 focus:outline-none focus:ring-red-300 dark:focus:ring-red-800 shadow-lg shadow-red-500/50 dark:shadow-lg dark:shadow-red-800/80 font-medium rounded-lg text-l py-2.5 text-center me-2 mb-2 w-40 d-flex ml-auto" @click="addSpace">Space</button>
    </div>

      <!-- Calculation History Menu -->
      <button @click="toggleHistory" class="text-white bg-gradient-to-r from-red-400 via-red-500 to-red-600 hover:bg-red-700 px-6 py-2 mt-4 rounded-lg shadow-md transition duration-300 ease-in-out focus:outline-none"> {{ showHistory ? 'Hide History' : 'Show History' }} </button>

    <div v-if="showHistory" class="absolute left-1/2 transform -translate-x-1/2 w-64 bg-red-600 text-white rounded-lg shadow-lg z-10 mt-6">
      <h3 class="text-white bg-gradient-to-r from-red-400 via-red-500 to-red-600 shadow-lg shadow-red-500/50 dark:shadow-lg dark:shadow-red-800/80 px-6 py-3 rounded-t-lg font-semibold"> History </h3>
      <ul class="divide-y divide-red-700">
      <li v-for=" (calculation, index) in history" :key="index" class="px-4 py-3 hover:bg-red-700 transition duration-300 ease-in-out"> {{ calculation }} </li>
      </ul>
    </div>
    </div>
</template>
<script>
import { numeric } from '@/data.js';

export default {
  name: "CalculatorContainer",
  data() {
    return {
          inputStr: '',
          numeric: numeric,
          history: [],
          showHistory: false
    };
  },
  methods: {
    handleButtonClick(button) {
      if (button.operation) {
          this.inputStr += button.operation;
      } 
      else {
          this.inputStr += button.text;
      }
    },
    validateInput(event) {
      if (event.key === ' ') {
          this.addSpace();
      } 
      else {
          this.inputStr = this.inputStr.replace(/[^-()\d/*+.π ]/g, '');
      }
    },
    clear() {
          this.inputStr = '';
    },
    remove() {
          this.inputStr = this.inputStr.slice(0, -1);
    },
    calculate() {
      try {
        if (!this.inputStr.trim()) {
          this.inputStr = '';
        return;
        }
        let expression = this.inputStr.replace(/%/g, '/100');
        // Add support for scientific functions
        const result = eval(expression);
        if (!isNaN(result) && result !== Infinity) {
          this.inputStr = result.toString();
          this.history.push(expression + ' = ' + result);
        } else {
          throw new Error('Invalid expression');
        }
      } 
        catch (error) {
          this.inputStr = error.message;
        }
    },
    toggleHistory() {
          this.showHistory = !this.showHistory;
    },
    addSpace() {
          this.inputStr += ' ';
    }
  }
};
</script>