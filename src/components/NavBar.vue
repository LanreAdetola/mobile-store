<template>
  <nav>
    <ul>
      <!-- Link to the Store section with smooth scrolling -->
      <li><a href="#store" @click.prevent="goTo('store')">Celestial_Events Online Store</a></li>
      <!-- Cart Overview -->
      <li class="cart-summary" @click="goTo('cart')">
        Cart ({{ cartItemCount }})
      </li>
    </ul>
  </nav>
</template>

<script>
export default {
  props: {
    cart: Array
  },
  computed: {
    cartItemCount() {
      return this.cart.reduce((count, item) => count + item.quantity, 0);
    }
  },
  methods: {
    goTo(section) {
      // Smooth scroll to the specified section by ID
      const element = document.getElementById(section);
      if (element) {
        element.scrollIntoView({ behavior: 'smooth' });
      }
    }
  }
};
</script>

<style scoped>
nav {
  background-color: #333; /* Dark background for the nav bar */
  color: #fff; /* White text color */
  padding: 0.5rem 1rem; /* Adjusted padding for a more compact look */
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2); /* Optional shadow for better separation */
}

ul {
  list-style: none; /* Remove bullet points from the list */
  display: flex; /* Display list items in a row */
  justify-content: space-between; /* Space items evenly */
  margin: 0; /* Remove default margin */
  padding: 0; /* Remove default padding */
}

li {
  margin: 0; /* Remove default margin from list items */
}

a {
  color: #fff; /* White text color for links */
  text-decoration: none; /* Remove underline from links */
  padding: 0.5rem 1rem; /* Padding around the link text */
  border-radius: 4px; /* Rounded corners for links */
  transition: background-color 0.3s; /* Smooth transition for hover effect */
}

a:hover {
  background-color: #555; /* Darker background color on hover */
}

.cart-summary {
  color: #fff; /* White text color for cart summary */
  cursor: pointer; /* Pointer cursor on hover */
  padding: 0.5rem 1rem; /* Padding around the cart summary */
  border-radius: 4px; /* Rounded corners */
  transition: background-color 0.3s; /* Smooth transition for hover effect */
}

.cart-summary:hover {
  background-color: #555; /* Darker background color on hover */
}

/* Responsive Design for mobile devices */
@media (max-width: 768px) {
  nav {
    padding: 0.5rem; /* Reduced padding on smaller screens */
  }

  ul {
    flex-direction: column; /* Stack navigation items vertically on smaller screens */
    align-items: center; /* Center items horizontally */
  }

  a, .cart-summary {
    padding: 0.5rem; /* Reduced padding for smaller screens */
  }
}
</style>
