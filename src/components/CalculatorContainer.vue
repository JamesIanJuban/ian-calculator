<template>
      <div class="container box justify-center items-center p-8">
        <!-- Calculator display -->
        <div class="display mb-6 mt-10 flex justify-center">
            <input type="text" v-model="inputStr" placeholder="Enter Expression" @keydown.enter="calculate" @input="validateInput" class="input-text w-full max-w-xl px-6 py-4 md:py-6 text-lg rounded-lg text-white border-2 border-gray-300 bg-red-600 placeholder-gray-100 focus:border-blue-500 focus:outline-none transition duration-300 ease-in-out">
        </div>    
   
    <!-- Scientific/Normal mode buttons -->
    <div class="grid grid-cols-5 gap-5 ml-6 mb-2">
      <button @click="toggleMode" class="text-white font-semibold text-sm py-2 w-24 bg-red-600 hover:bg-red-700 rounded-lg focus:outline-none shadow-md transition duration-300 ease-in-out">{{ mode === 'Normal' ? 'Scientific' : 'Normal' }}</button>
    </div>
        <!-- Operation buttons -->  
        <div class="grid grid-cols-5 gap-4 px-6 py-4">

            <button v-for="item in numeric" :key="item.text" class="text-red-500 py-2 rounded-lg bg-gray-200 hover:bg-gray-300" @click="handleButtonClick(item)">{{ item.text }}</button>  

            <button class="text-white font-semibold text-sm py-2 bg-red-600 hover:bg-red-700 rounded-lg focus:outline-none shadow-md transition duration-300 ease-in-out" @click="remove">←</button>
            <button class="text-white font-semibold text-sm py-2 bg-red-600 hover:bg-red-700 rounded-lg focus:outline-none shadow-md transition duration-300 ease-in-out" @click="clear">AC</button>
            <button class="text-white font-semibold text-sm py-2 bg-red-600 hover:bg-red-700 rounded-lg focus:outline-none shadow-md transition duration-300 ease-in-out" @click="calculate">=</button>
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
      mode: 'Normal', // Default mode
    };
  },
  methods: {
    handleButtonClick(button) {
      if (button.operation) {
          this.inputStr += button.operation;
      } else {
          this.inputStr += button.text;
      }
    },
    validateInput() {
          this.inputStr = this.inputStr.replace(/[^-()\d/*+.π]|%/g, '');
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
        const result = Function('"use strict";return (' + expression + ')')();
        if (!isNaN(result) && result !== Infinity) {
          this.inputStr = result.toString();
        } else {
          throw new Error('Invalid expression');
        }
      } catch (error) {
          this.inputStr = error.message;
      }
    },
    toggleMode() {
          this.mode = this.mode === 'Normal' ? 'Scientific' : 'Normal';
    }
  }
};
</script>
  
  