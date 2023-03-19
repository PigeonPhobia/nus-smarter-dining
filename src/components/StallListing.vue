<template>
  <v-row>
    <v-col v-for="stall in stalls" :key="stall" cols="6">
      <v-card @click="onClickStall(stall)" min-height="200">
        <v-card-text>{{ stall }}</v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>
  
<script setup>
  const emit = defineEmits(["error-added", "stall-selected"])
  const stalls = [
    "Ban Mian",
    "Japanese Ramen", 
    "Indian Fusion", 
    "Seafood Pao Fan",
    "Mala Pot",
    "Vegeterian",
    "Mixed Veg Rice",
    "Fried Rice",
    "Curry Rice Set",
    "Take n Go",
    "Beverage"
  ]
  function onClickStall (stall) {
    console.log("Click stall", stall)
    if (stall !== "Fried Rice" && stall !== "Beverage") { 
      emit("error-added")
    } else {
      emit("stall-selected", stall)
    }
  }
</script>