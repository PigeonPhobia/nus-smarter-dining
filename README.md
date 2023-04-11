# NUS Smarter Dining

## Hosted UIs
You can access our experiment apparatus from following url:

https://pigeonphobia.github.io/nus-smarter-dining/?header=small&cart=tl&activation=auto&food=ab&user=abc123

### parameter definition:
header: whether the header is big or small, controlling the scrollable range; possible values: small, large

cart: location and size of cart button; possible values: ts, tl, bs, bl (t for top, b for bottom, s for small, l for large)

activation: activation of cart page; possible values: auto, manual

food: the food combination we require participant to order; possible values: ab, cd, ef

user: the user identifier for logging

### food combinations:
ab: "Plant-based Tomato Mushroom Meatball Rice Bowl" from Fired Rice stall, "Hot Pearl Barley" from Beverages stall

cd: "Egg Fried Rice" from Fired Rice stall, "Iced Lime Juice" from Beverages stall

ef: "Beef Bulgogi with Tempura Rice Set" from Fired Rice stall, "Iced Wintermelon" from Beverages stall

## Brief description of files and folders
```
├── public
│   └── favicon.ico (Favorite icon)
├── src
│   ├── components
│   │   ├── AddFoodPage.vue (It displays the page for user to add the selected food.)
│   │   ├── CanteenListing.vue (It displays the canteens for user to select.)
│   │   ├── CartListing.vue (It displays the ordered food items and provides the button to check out.)
│   │   ├── FoodListing.vue (It displays the food items based on the selected stall.)
│   │   └── StallListing.vue (It displays the stalls based on the selected canteen.)
│   ├── App.vue (The backbone of our mobile app, it defines the app header, app content and the layout. It keep tracks of the current app page and handles the final logging of data.)
│   └── main.js (defines the Vue and Vuetify context)
├── index.html (Nodejs backbone html)
├── logging.js (js file to log user experiment data)
├── vite.config.js (Vuejs project definition file)
├── package.json (Nodejs project definition file)
├── package-lock.json (lock file for package.json)
├── README.md (README file)
├── .gitattributes
└── .gitignore
```

