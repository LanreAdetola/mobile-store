<template>
  <div class="store-item">
    <!-- Div for the item image -->
    <div class="image-container">
      <img :src="require(`@/assets/${item.image}`)" :alt="item.name" class="item-image" />
    </div>
    <!-- Div for item details -->
    <div class="item-details">
      <h2>{{ item.name }}</h2>
      <p>Price: {{ item.price }} XAF</p>
      <!-- Button to add the item to the cart -->
      <button @click="addToCart">Add to Cart</button>
    </div>
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
  display: flex; /* Use flexbox for layout */
  align-items: center; /* Vertically center items */
  gap: 1rem; /* Space between the image and details */
}

/* Style for the image container */
.image-container {
  flex-shrink: 0; /* Prevent the image container from shrinking */
}

/* Style for the item image */
.item-image {
  width: 300px; /* Fixed width for the image */
  height: auto; /* Keep the aspect ratio */
}

/* Style for the item details container */
.item-details {
  flex: 1; /* Allow the details to take up remaining space */
  text-align: left; /* Left align the item details */
}

/* Button styles */
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
