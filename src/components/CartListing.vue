<template>
  <div>
    <v-alert v-for="food in Object.keys(cartFood)" :text="food" style="margin-top: 5px;"></v-alert>
    <v-btn @click="onCheckOut" color="orange" style="margin-top: 22px;">Check Out</v-btn>
    <v-alert v-if="showError" text="Food items are incorrect!" type="error" style="margin-top: 5px;"></v-alert>
  </div>
</template>
  
<script setup>
  import { ref, toRefs } from 'vue';
  const props = defineProps({
    cartFood: Object,
  });
  const { cartFood } = toRefs(props);
  console.log('Current cart food is', cartFood.value)
  const emit = defineEmits(["check-out"])
  const showError = ref(false)

  const foodMap = {
    "ab": ["Plant-based Tomato Mushroom Meatball Rice Bowl", "Hot Pearl Barley"],
    "cd": ["Egg Fried Rice", "Iced Lime Juice"],
    "ef": ["Beef Bulgogi with Tempura Rice Set", "Iced Wintermelon"]
  }
  function onCheckOut () {
    const urlParams = new URLSearchParams(window.location.search)
    const foodKey = urlParams.get("food")
    const allowedFoods = foodMap[foodKey]
    const isInCart = k => cartFood.value[k] > 0
    if (allowedFoods && allowedFoods.every(isInCart)) {
      console.log("Checked out!")
      emit("check-out")
    } else {
      console.log("Cart food incorrect!")
      console.log("Show cart error!")
      showError.value = true
    }
  }
</script>