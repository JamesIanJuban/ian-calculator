<template>
  <article class="text-center"> 
    <h1 class="text-4xl text-white bg-gradient-to-br from-gray-800 to-gray-900 mt-10 font-bold">Scientific Calculator</h1>
      <CalculatorContainer/>
  </article>
</template>
  
<script>
import CalculatorContainer from './components/CalculatorContainer.vue'


export default {
    name: 'App',
    components: {
    CalculatorContainer,
  }
}
</script>