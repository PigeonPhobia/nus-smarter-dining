<template>
  <v-app>
    <v-app-bar color="orange">
      <v-btn>Back</v-btn>
      <v-spacer></v-spacer>
      <v-btn @click="onClickCart">Cart</v-btn>
    </v-app-bar>

    <v-container>
      <v-row>
        <v-spacer></v-spacer>
        <v-col v-for="canteen in canteens" :key="canteen" cols="6">
          <v-card @click="onClickCard(canteen)" style="height: 250px;">
            <v-card-text>{{ canteen }}</v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script setup>
  let error = 0
  const canteens = [
    "The Terrace",
    "The Summit", 
    "PGPR", 
    "Frontier (Non Aircon)",
    "Frontier (Aircon)",
    "Techno Edge",
    "The Deck"
  ]
  function onClickCart () {
    console.log("Click Cart!!!")
  }
  function onClickCard (canteen) {
    if (canteen !== "The Terrace") { error++ }
    console.log("Click Card", canteen, "! Current error: ", error)
  }
</script>