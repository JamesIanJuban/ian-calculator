<template>
    <div class="calculator justify-center items-center">
        <!-- Calculator display -->
        <div class="display mb-6 mt-12">
            <input type="text" v-model="inputStr" placeholder="Enter Expression" @keydown.enter="calculate" @input="validateInput" class="input-text w-4/5 p-3 text-lg rounded-lg border-2 border-gray-300 bg-gray-100 text-gray-800 focus:border-blue-500 focus:outline-none transition duration-300 ease-in-out">
        </div>
        <!-- Operation buttons -->  
        <div class="grid grid-cols-4 gap-2">
            <button v-for="item in numeric" :key="item.text" class="btn" @click="handleButtonClick(item)">{{ item.text }}</button>
            <button class="" @click="calculate">Calculate</button>
            <button class="" @click="clear">Clear</button>
            <button class="focus:outline-none text-white bg-purple-700 hover:bg-purple-800 focus:ring-4 focus:ring-purple-300 font-medium rounded-lg text-sm px-5 py-2.5 mb-2 dark:bg-purple-600 dark:hover:bg-purple-700 dark:focus:ring-purple-900" @click="remove">Backspace</button>
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
        numeric: numeric
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
      }
    }
  };
  </script>
  
  