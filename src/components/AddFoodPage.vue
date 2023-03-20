<template>
  <div v-if="currentFood !== ''">
    <v-alert :text="currentFood"></v-alert>
    <v-btn @click="onAddFood" color="orange" style="margin-top: 22px;">Add</v-btn>
    <v-alert v-show="added" text="Added to cart" type="success" style="margin-top: 10px;"></v-alert>
  </div>
  <v-alert v-else text="Not included in experiment" type="warning"></v-alert>
</template>
  
<script setup>
  import { ref, toRefs } from 'vue';
  const props = defineProps({
    currentFood: String,
  });
  const { currentFood } = toRefs(props);
  console.log('Current food is', currentFood.value)
  const emit = defineEmits(["food-added"])
  let added = ref(false)
  function onAddFood () {
    console.log("Click add food", currentFood.value)
    added.value = true
    emit("food-added", currentFood.value)
  }
</script>