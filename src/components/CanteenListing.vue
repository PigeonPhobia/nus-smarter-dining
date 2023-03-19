<template>
  <v-row>
    <v-col v-for="canteen in canteens" :key="canteen" cols="6">
      <v-card @click="onClickCanteen(canteen)" min-height="200">
          <v-card-text>{{ canteen }}</v-card-text>
        </v-card>
    </v-col>
  </v-row>
</template>

<script setup>
  const emit = defineEmits(["error-added", "canteen-selected"])
  const canteens = [
    "The Terrace",
    "The Summit", 
    "PGPR", 
    "Frontier (Non Aircon)",
    "Frontier (Aircon)",
    "Techno Edge",
    "The Deck"
  ]
  function onClickCanteen (canteen) {
    console.log("Click Card", canteen)
    if (canteen !== "The Terrace") { 
      emit("error-added")
    } else {
      emit("canteen-selected")
    }
  }
</script>