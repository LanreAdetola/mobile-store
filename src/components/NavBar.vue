<template>
  <nav>
    <ul>
      <!-- Link to the Store section with smooth scrolling -->
      <li><a href="#store" @click.prevent="goTo('store')">Store</a></li>
      <!-- You can add more navigation links here in the future -->
    </ul>
  </nav>
</template>

<script>
export default {
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
  padding: 1rem; /* Padding around the nav bar */
}

ul {
  list-style: none; /* Remove bullet points from the list */
  display: flex; /* Display list items in a row */
  justify-content: center; /* Center items horizontally */
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
}

a:hover {
  background-color: #555; /* Darker background color on hover */
}
</style>
