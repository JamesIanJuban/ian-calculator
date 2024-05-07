<template>
  <article class="text-center"> 
    <h1 class="text-4xl text-transparent bg-gradient-to-r from-red-400 to-red-600 bg-clip-text mt-8 font-bold">Scientific Calculator</h1>
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