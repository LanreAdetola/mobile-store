<template>
  <div id="app">
    <NavBar />
    <div id="main-content">
      <!-- Store section -->
      <div id="store">
        <ItemList :items="items" :cart="cart" @add-to-cart="addToCart" />
      </div>
      <!-- Cart section -->
      <div id="cart">
        <CartComp :cart="cart" @remove-from-cart="removeFromCart" @update-cart="updateCart" />
      </div>
    </div>
    <FooterBar />
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue';
import ItemList from './components/ItemList.vue';
import CartComp from './components/CartComp.vue';
import FooterBar from './components/FooterBar.vue';

export default {
  components: {
    NavBar,
    ItemList,
    CartComp,
    FooterBar
  },
  data() {
    return {
      items: [
        { id: 1, name: 'Item 1', price: 10, image: require('@/assets/basket1.png') },
        { id: 2, name: 'Item 2', price: 20, image: require('@/assets/basket1.png') },
        { id: 3, name: 'Item 3', price: 30, image: require('@/assets/basket1.png') },
        { id: 4, name: 'Item 4', price: 50, image: require('@/assets/basket1.png') },
      ],
      cart: []
    };
  },
  methods: {
    addToCart(item) {
      const found = this.cart.find(cartItem => cartItem.id === item.id);
      if (found) {
        found.quantity += 1;
      } else {
        this.cart.push({ ...item, quantity: 1 });
      }
    },
    removeFromCart(itemId) {
      const index = this.cart.findIndex(item => item.id === itemId);
      if (index !== -1) {
        this.cart.splice(index, 1);
      }
    },
    updateCart(updatedCart) {
      this.cart = updatedCart; // Update cart with the latest changes
    }
  }
};
</script>

<style>
/* Base styling for the main content container */
#main-content {
  display: flex; /* Use flexbox for layout */
  justify-content: space-between; /* Space items evenly */
  padding: 1rem; /* Add some padding around the content */
}

#store {
  flex: 3; /* Takes up 3 parts of the space */
  margin-right: 1rem; /* Space between store and cart */
}

#cart {
  flex: 1; /* Takes up 1 part of the space */
  border: 1px solid #ddd; /* Optional border for better visibility */
  border-radius: 5px; /* Rounded corners for the cart */
  padding: 1rem; /* Padding inside the cart */
}

/* Responsive Design for tablets and mobile devices */
@media (max-width: 768px) {
  #main-content {
    flex-direction: column; /* Stack store and cart vertically on tablets */
  }

  #store {
    margin-right: 0; /* Remove margin when stacked */
    margin-bottom: 1rem; /* Add space below store when stacked */
  }

  #cart {
    border: none; /* Optional: Remove border on smaller screens */
    padding: 0.5rem; /* Adjust padding for smaller screens */
  }
}

/* Responsive Design for very small screens, like iPhones */
@media (max-width: 414px) {
  #main-content {
    flex-direction: column; /* Stack store and cart vertically on very small screens */
  }

  #store, #cart {
    width: 100%; /* Ensure both sections take full width */
    margin: 0; /* Remove any extra margins */
  }
}
</style>
