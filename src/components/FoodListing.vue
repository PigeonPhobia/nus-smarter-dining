<template>
  <v-row v-if="currentStall === 'Fried Rice' || currentStall === 'Beverage'">
    <v-col v-for="food in foods" :key="food" cols="12">
      <v-card variant="tonal" @click="onClickFood(food)">
        <v-card-text>{{ food }}</v-card-text>
      </v-card>
    </v-col>
  </v-row>
  <v-alert v-else text="Not included in experiment" type="warning"></v-alert>
</template>
  
<script setup>
  import { toRefs } from 'vue';
  const props = defineProps({
    currentStall: String,
  });
  const { currentStall } = toRefs(props);
  console.log('Current stall is', currentStall.value)
  const emit = defineEmits(["error-added", "food-selected"])
  const foods = [
    "Plant-based Teriyaki Unagi Rice Bowl",
    "Plant-based Tomato Mushroom Meatball Rice Bowl",
    "Egg Fried Rice",
    "Shrimp Fried Rice", 
    "Black Pepper Beef Rice"
  ]
  function onClickFood (food) {
    console.log("Click food", food)
    const allowedFoods = ["Plant-based Tomato Mushroom Meatball Rice Bowl", "Egg Fried Rice"]
    if (!allowedFoods.includes(food)) { 
      emit("error-added")
      emit("food-selected", "")
    } else {
      emit("food-selected", food)
    }
  }
</script>