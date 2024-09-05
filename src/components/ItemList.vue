<template>
  <div>
    <h1>Gift Baskets</h1>
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
    items: Array, // Items passed as a prop from parent (App.vue)
    cart: Array   // Cart also passed as a prop from parent
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
