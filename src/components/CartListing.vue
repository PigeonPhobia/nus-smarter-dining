<template>
  <div>
    <v-alert v-for="food in Object.keys(cartFood)" :text="food" style="margin-top: 5px;"></v-alert>
    <v-btn @click="onCheckOut" color="orange" style="margin-top: 22px;">Check Out</v-btn>
  </div>
</template>
  
<script setup>
  import { toRefs } from 'vue';
  const props = defineProps({
    cartFood: Object,
  });
  const { cartFood } = toRefs(props);
  console.log('Current cart food is', cartFood.value)
  const emit = defineEmits(["check-out"])
  function onCheckOut () {
    console.log("Checked out!")
    emit("check-out")
  }
</script>