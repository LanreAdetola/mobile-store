<template>
  <div>
    <h1>Store</h1>
    <!-- Display a list of items -->
    <StoreItem
      v-for="item in items"
      :key="item.id"
      :item="item"
      @add-to-cart="addToCart"
    />
  </div>
</template>

<script>
import StoreItem from './StoreItem.vue';

export default {
  components: { StoreItem },
  props: {
    cart: Array // Passes the cart array as a prop
  },
  data() {
    return {
      items: [
        { id: 1, name: 'Item 1', price: 10 },
        { id: 2, name: 'Item 2', price: 20 },
        { id: 3, name: 'Item 3', price: 30 },
        { id: 4, name: 'Item 4', price: 50 },
        // Add more items as needed
      ]
    };
  },
  methods: {
    addToCart(item) {
      // Emits an event to notify the parent component to add the item to the cart
      this.$emit('add-to-cart', item);
    }
  }
};
</script>

<style scoped>
/* Add any component-specific styles here */
</style>
