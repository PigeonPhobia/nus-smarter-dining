<template>
  <v-row v-if="currentCanteen === 'The Terrace'">
    <v-col v-for="stall in stalls" :key="stall" cols="6">
      <v-card variant="tonal" @click="onClickStall(stall)" min-height="200">
        <v-card-text>{{ stall }}</v-card-text>
      </v-card>
    </v-col>
  </v-row>
  <v-alert v-else text="Not included in experiment" type="warning"></v-alert>
</template>
  
<script setup>
  import { toRefs } from 'vue';
  const props = defineProps({
    currentCanteen: String,
  });
  const { currentCanteen } = toRefs(props);
  console.log('Current canteen is', currentCanteen.value)
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
      emit("stall-selected", "")
    } else {
      emit("stall-selected", stall)
    }
  }
</script>