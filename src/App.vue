<template>
  <v-app>
    <v-app-bar color="orange">
      <v-btn @click="onBackButton">Back</v-btn>
      <v-spacer></v-spacer>
      <v-btn @click="onClickCart">Cart</v-btn>
    </v-app-bar>

    <v-container style="padding-top: 100px;">
      <CanteenListing 
        v-if="page === 'canteen'" 
        @error-added="onErrorAdded" 
        @canteen-selected="onCanteenSelected"
      >
      </CanteenListing>
      <StallListing
        v-else-if="page === 'stall'" 
        @error-added="onErrorAdded" 
        @stall-selected="onStallSelected"
      >
      </StallListing>
      <FoodListing
        v-else-if="page === 'food'"
        :currentStall="currentStall" 
        @error-added="onErrorAdded" 
        @food-selected="onFoodSelected"
      >
      </FoodListing>
    </v-container>
  </v-app>
</template>

<script setup>
  import { ref } from 'vue'
  import CanteenListing from './components/CanteenListing.vue';
  import FoodListing from './components/FoodListing.vue';
  import StallListing from './components/StallListing.vue';

  const pages = ["canteen", "stall", "food", "cart"]
  let page = ref("canteen")
  function onBackButton () {
    console.log("Click Back!!!")
    if (page.value === 'canteen') {
      console.log("Already in canteen listing, break")
    }
    const idx = pages.indexOf(page.value)
    console.log("Current page no", idx)
    page.value = pages[idx - 1]
    console.log("Back to page", pages[idx - 1])
  }

  let error = 0
  function onErrorAdded () {
    error++
    console.log("Error added! Error: ", error)
  }
  
  function onCanteenSelected () {
    console.log("Go to stall page")
    page.value = "stall"
  }

  let currentStall = ref("")
  function onStallSelected (stall) {
    console.log("Before Select Stall,", currentStall.value)
    currentStall.value = stall
    console.log("After Select Stall,", currentStall.value)
    console.log("Go to food page")
    page.value = "food"
  }

  let currentFood = ref("")
  function onFoodSelected (food) {
    console.log("Before Select Food,", currentFood.value)
    currentFood.value = food
    console.log("After Select Food,", currentFood.value)
  }

  function onClickCart () {
    console.log("Click Cart!!!")
  }
</script>