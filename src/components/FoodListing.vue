<template>
  <v-row v-if="currentStall === 'Fried Rice' || currentStall === 'Beverages'">
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
  const foods = currentStall.value === "Fried Rice" ? [
    "Plant-based Teriyaki Unagi Rice Bowl",
    "Plant-based Tomato Mushroom Meatball Rice Bowl",
    "Egg Fried Rice",
    "Shrimp Fried Rice", 
    "Black Pepper Beef Rice Bowl",
    "Chicken Cutlet Fried Rice",
    "Mini Prok Cutlet Fried Rice",
    "Beef Bulgogi with Tempura Rice Set",
    "Teriyaki Chicken with Tempura Rice Set",
    "Basil Leave Minced Meat Rice Bowl",
    "Black Pepper Chicken Rice Bowl",
    "Gong Bao Chicken Rice Bowl",
    "Stir-fried Ginger and Scallion Prok Rice Bowl",
    "Sweet and Sour Pork Rice Bowl"
  ] : [
    "Bubble Tea",
    "Hot Pearl Barley",
    "Ice Lemon Tea",
    "Iced Pearl Barley",
    "Iced Waterchestnut",
    "Coffee-O",
    "Coffee-O Kosong",
    "Tea-O",
    "Tea-O Kosong",
    "Coffee",
    "Tea",
    "Coffee-C",
    "Coffee-C Kosong",
    "Milo",
    "Tea-C Kosong",
    "Yuan Yang",
    "Iced Lime Juice",
    "Iced Wintermelon",
    "Soya"
  ]

  const foodMap = {
    "ab": ["Plant-based Tomato Mushroom Meatball Rice Bowl", "Hot Pearl Barley"],
    "cd": ["Egg Fried Rice", "Iced Lime Juice"],
    "ef": ["Beef Bulgogi with Tempura Rice Set", "Iced Wintermelon"]
  }
  function onClickFood (food) {
    console.log("Click food", food)
    const urlParams = new URLSearchParams(window.location.search)
    const foodKey = urlParams.get("food")
    const allowedFoods = foodMap[foodKey] || []
    if (!allowedFoods.includes(food)) { 
      emit("error-added")
      emit("food-selected", "")
    } else {
      emit("food-selected", food)
    }
  }
</script>