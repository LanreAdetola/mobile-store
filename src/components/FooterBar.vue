<template>
    <footer>
      <p>&copy; {{ currentYear }} Celestial_Events | Powered by <span>NovemberCodes365</span></p>
    </footer>
  </template>
  
  <script>
  export default {
    data() {
      return {
        currentYear: new Date().getFullYear() // Automatically get the current year
      };
    }
  };
  </script>
  
  <style scoped>
  footer {
  background-color: #333; /* Matching NavBar */
  color: #fff;
  padding: 0.5rem;
  text-align: center;
  position: fixed; /* Ensure footer sticks to the bottom */
  bottom: 0;
  width: 100%;
  box-shadow: 0 -2px 4px rgba(0, 0, 0, 0.2); /* Optional shadow */
}

  
  footer p {
    margin: 0; /* Remove default margin */
  }
  
  footer span {
    font-weight: bold; /* Highlight "Powered by" text */
  }
  
  @media (max-width: 768px) {
    footer {
      padding: 0.5rem; /* Adjust padding on smaller screens */
    }
  }
  </style>
  