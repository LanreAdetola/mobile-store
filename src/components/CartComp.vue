<template>
  <div>
    <h2>Shopping Cart</h2>
    <ul class="cart-list">
      <li v-for="item in cart" :key="item.id" class="cart-item">
        <span class="item-info">
          {{ item.name }} - {{ item.price }} XAF x
        </span>
        <div class="item-controls">
          <button @click="decreaseQuantity(item)" aria-label="Decrease quantity">-</button>
          <span>{{ item.quantity }}</span>
          <button @click="increaseQuantity(item)" aria-label="Increase quantity">+</button>
          <button @click="removeFromCart(item.id)" aria-label="Remove item">Remove</button>
        </div>
      </li>
    </ul>
    <div v-if="cart.length" class="total">
      <p>Total: {{ total }} XAF</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    cart: Array
  },
  computed: {
    total() {
      return this.cart.reduce((acc, item) => acc + item.price * item.quantity, 0);
    }
  },
  methods: {
    increaseQuantity(item) {
      item.quantity += 1;
      this.$emit('update-cart', this.cart); // Notify parent component of cart update
    },
    decreaseQuantity(item) {
      if (item.quantity > 1) {
        item.quantity -= 1;
        this.$emit('update-cart', this.cart); // Notify parent component of cart update
      } else {
        this.removeFromCart(item.id);
      }
    },
    removeFromCart(itemId) {
      this.$emit('remove-from-cart', itemId);
    }
  }
};
</script>

<style scoped>
/* Styling for the cart list */
.cart-list {
  list-style-type: none; /* Remove default list styling */
  padding: 0; /* Remove default padding */
}

.cart-item {
  display: flex; /* Use flexbox for layout */
  justify-content: space-between; /* Space between item info and controls */
  align-items: center; /* Vertically center items */
  margin-bottom: 0.5rem; /* Space between items */
  border-bottom: 1px solid #ddd; /* Border for separation */
  padding: 0.5rem 0; /* Padding for items */
}

.item-info {
  flex: 1; /* Allow item info to take up available space */
}

.item-controls {
  display: flex; /* Use flexbox for controls layout */
  align-items: center; /* Vertically center controls */
  gap: 0.5rem; /* Space between controls */
}

button {
  background-color: #28a745; /* Green background for buttons */
  color: #fff; /* White text color */
  border: none; /* Remove default border */
  padding: 0.5rem; /* Padding inside the button */
  border-radius: 5px; /* Rounded corners */
  cursor: pointer; /* Pointer cursor on hover */
}

button:hover {
  background-color: #218838; /* Darker green on hover */
}

.total {
  margin-top: 1rem; /* Space above the total */
  font-weight: bold; /* Emphasize the total amount */
}
</style>
