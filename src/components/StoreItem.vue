<template>
  <div class="store-item">
    <!-- Display item name and price -->
    <h2>{{ item.name }}</h2>
    <p>Price: {{ item.price }} XAF</p>
    <!-- Button to add the item to the cart -->
    <button @click="addToCart">Add to Cart</button>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true // Ensures that an item object is always passed
    }
  },
  methods: {
    addToCart() {
      // Emits an event with the current item to the parent component
      this.$emit('add-to-cart', this.item);
    }
  }
};
</script>

<style scoped>
/* Scoped styles for the StoreItem component */
.store-item {
  border: 1px solid #ddd; /* Light border around each item */
  border-radius: 5px; /* Rounded corners */
  padding: 1rem; /* Padding inside the item container */
  margin-bottom: 1rem; /* Margin between items */
  text-align: center; /* Center text alignment */
}

button {
  background-color: #28a745; /* Green background for the button */
  color: #fff; /* White text color */
  border: none; /* Remove default border */
  padding: 0.5rem 1rem; /* Padding inside the button */
  border-radius: 5px; /* Rounded corners for the button */
  cursor: pointer; /* Pointer cursor on hover */
}

button:hover {
  background-color: #218838; /* Darker green on hover */
}
</style>
