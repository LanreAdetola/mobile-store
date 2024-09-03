<template>
  <div>
    <h2>Shopping Cart</h2>
    <ul>
      <li v-for="item in cart" :key="item.id">
        {{ item.name }} - {{ item.price }}  x 
        <button @click="decreaseQuantity(item)">-</button>
        {{ item.quantity }}
        <button @click="increaseQuantity(item)">+</button>
        <button @click="removeFromCart(item.id)">Remove</button>
      </li>
    </ul>
    <div v-if="cart.length">
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
/* Add some basic styling for buttons */
button {
  margin: 0 5px;
}
</style>
