<script setup>
import BasicCalculator from "./components/BasicCalculator.vue";
import ScientificCalculator from "./components/ScientificCalculator.vue";
</script>

<template>
  <span @click="toggle()" class="toggle-btn">
    {{toggleText}}
  </span>
  <div v-if="advancedOptions">
    <ScientificCalculator />
  </div>
  <div v-else>
    <BasicCalculator />
  </div>
</template>

<script>
export default {
  data() {
    return {
      advancedOptions: false,
      toggleText: 'Ba'
    }
  }, methods: {
    toggle() {
      if (this.advancedOptions === false) {
        this.advancedOptions = true;
        this.toggleText = 'Sc'
      } else {
        this.advancedOptions = false;
        this.toggleText = 'Ba'
      }
    }
  }
}
</script>

<style>
  .toggle-btn {
    width: 150px;
    height: 0px;
    float: left;
  } body{
    background-color: antiquewhite;
  }
</style>