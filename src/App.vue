<template>
  <v-app>
    <v-app-bar color="orange" :style="headerStyle">
      <v-btn @click="onBackButton">Back</v-btn>
      <v-spacer></v-spacer>
      <v-btn v-if="cartBtnTop" :size="cartBtnSize" @click="onClickCart">Cart</v-btn>
    </v-app-bar>

    <v-container :style="containerStyle">
      <CanteenListing 
        v-if="page === 'canteen'"
        @error-added="onErrorAdded"
        @canteen-selected="onCanteenSelected"
      >
      </CanteenListing>
      <StallListing
        v-else-if="page === 'stall'" 
        :currentCanteen="currentCanteen" 
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
      <AddFoodPage
        v-else-if="page === 'add-food'"
        :currentFood="currentFood" 
        @food-added="onFoodAdded"
      >
      </AddFoodPage>
      <CartListing
        v-else-if="page === 'cart'"
        :cartFood="cartFood" 
        @check-out="onCheckOut"
      >
      </CartListing>
      <v-alert v-else-if="page === 'final'" type="success" :text="finalMessage"></v-alert>
      <v-btn 
        v-if="!cartBtnTop"
        color="orange" 
        :size="cartBtnSize" 
        @click="onClickCart" 
        style="position: fixed; right: 20px; bottom: 20px;">
        Cart
      </v-btn>
    </v-container>
  </v-app>
</template>

<script setup>
  import { ref } from 'vue'
  import AddFoodPage from './components/AddFoodPage.vue';
  import CanteenListing from './components/CanteenListing.vue';
  import CartListing from './components/CartListing.vue';
  import FoodListing from './components/FoodListing.vue';
  import StallListing from './components/StallListing.vue';
  
  const urlParams = new URLSearchParams(window.location.search)
  const header = urlParams.get("header")
  const headerStyle = header === "small" ? "height: 100px;" : "height: 200px;"
  const containerStyle = header === "small" ? "padding-top: 120px;" : "padding-top: 220px;"

  const cartBtn = urlParams.get("cart")
  const cartBtnSize = ['ts', 'bs'].includes(cartBtn) ? "small" : "x-large"
  const cartBtnTop = ['ts', 'tl'].includes(cartBtn)

  const activation = urlParams.get("activation")
  const gotoCart = activation === "auto"

  const pages = ["canteen", "stall", "food", "add-food", "cart", "final"]
  let page = ref("canteen")
  function onBackButton () {
    console.log("Click Back!!!")
    if (page.value === 'canteen') {
      console.log("Already in canteen listing, break")
      return
    }
    if (page.value === 'cart') {
      console.log("Current page is cart")
      if (currentFood.value !== "") {
        console.log("Food is not empty")
        page.value = "food"
        console.log("Back to food page")
      } else {
        console.log("Food is empty")
        page.value = "canteen"
        console.log("Back to canteen page")
      }
      return
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
  
  let currentCanteen = ref("")
  function onCanteenSelected (canteen) {
    console.log("Before Select Canteen,", currentCanteen.value)
    currentCanteen.value = canteen
    console.log("After Select Canteen,", currentCanteen.value)
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
    console.log("Go to add food page")
    page.value = "add-food"
  }

  let cartFood = ref({})
  function onFoodAdded (food) {
    console.log("Food added!", food)
    cartFood.value[food] = 1
    console.log("Current food in cart:", cartFood.value)
    if (gotoCart) {
      console.log("Auto activation: go to cart page")
      page.value = "cart"
    } else {
      console.log("Manual activation: go to food page")
      page.value = "food"
    }
  }

  function onClickCart () {
    console.log("Click Cart!!!")
    console.log("Go to cart page")
    page.value = "cart"
  }

  const foodKey = urlParams.get("food")
  let finalMessage = ref("Please wait for final logging...")
  const startTime = new Date().getTime()
  function onCheckOut () {
    console.log("Final Check Out, go to final page, log total time")

    const endTime = new Date().getTime()
    page.value = "final"
    loggingjs.logEvent(null, 'final-result-log', {
		  header,
		  cart: cartBtn,
		  activation,
		  food: foodKey,
      timeTaken: (endTime - startTime) / 1000,
      error
	  });
    setTimeout(() => {
      console.log("logging done, change message")
      finalMessage.value = "Logging is done, please close the tab and continue the experiment. Thank you!"
    }, 3000)
    
  }
</script>