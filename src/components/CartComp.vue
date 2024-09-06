<template>
  <div>
    <h2>Shopping Cart</h2>
    
    <!-- Show when cart is empty -->
    <p v-if="!cart.length">Your cart is empty.</p>
    
    <!-- Show cart items when available -->
    <ul v-else class="cart-list">
      <li v-for="item in cart" :key="item.id" class="cart-item">
        <span class="item-info">
          {{ item.name }} - {{ item.price }} XAF
        </span>
        <div class="item-controls">
          <button @click="decreaseQuantity(item)" aria-label="Decrease quantity">-</button>
          <span class="quantity">{{ item.quantity }}</span>
          <button @click="increaseQuantity(item)" aria-label="Increase quantity">+</button>
          <button @click="removeFromCart(item.id)" aria-label="Remove item">Remove</button>
        </div>
      </li>
    </ul>
    
    <!-- Show total price when items are in the cart -->
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
  padding: 0.5rem 1rem; /* Padding for items */
}

.item-info {
  flex: 2; /* Allow item info to take up more space */
  font-size: 1rem; /* Ensure font size is legible */
  color: #333; /* Darker color for better contrast */
}

.item-controls {
  display: flex; /* Use flexbox for controls layout */
  align-items: center; /* Vertically center controls */
  gap: 0.5rem; /* Space between controls */
}

.quantity {
  font-weight: bold; /* Make quantity more noticeable */
  font-size: 1rem; /* Adjust font size for readability */
  color: #333; /* Darker color for better contrast */
}

button {
  background-color: #28a745; /* Green background for buttons */
  color: #fff; /* White text color */
  border: none; /* Remove default border */
  padding: 0.5rem 0.75rem; /* Padding for buttons */
  border-radius: 5px; /* Rounded corners */
  cursor: pointer; /* Pointer cursor on hover */
  font-size: 1rem; /* Ensure font size is legible on mobile */
}

button:hover {
  background-color: #218838; /* Darker green on hover */
}

.total {
  margin-top: 1rem; /* Space above the total */
  font-weight: bold; /* Emphasize the total amount */
  font-size: 1.2rem; /* Larger font size for the total */
  color: #333; /* Darker color for better contrast */
}

/* Responsive Design for mobile devices */
@media (max-width: 768px) {
  .cart-item {
    flex-direction: column; /* Stack item info and controls vertically on small screens */
  }

  .item-controls {
    flex-direction: column; /* Stack controls vertically on small screens */
    align-items: stretch; /* Make controls take full width */
  }

  button {
    width: 100%; /* Make buttons full width on small screens */
    padding: 0.5rem; /* Adjust padding for smaller screens */
    font-size: 0.9rem; /* Adjust font size for smaller screens */
  }

  .quantity {
    font-size: 0.9rem; /* Adjust font size for smaller screens */
  }
}

@media (max-width: 414px) {
  .item-info {
    font-size: 0.9rem; /* Adjust font size for very small screens */
  }

  button {
    padding: 0.5rem; /* Maintain button size on very small screens */
    font-size: 0.9rem; /* Ensure buttons are appropriately sized */
  }
}
</style>
