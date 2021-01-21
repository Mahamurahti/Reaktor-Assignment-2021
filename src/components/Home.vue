<template>
  <div>
    <!-- Catch emits from the Navigation component -->
    <Navigation @product:call="printProduct"
                @product:load="loadingScreen"
                @product:head="updateHead"
                @content:entry="loadEntry" />
    <div class="home">
      <h1>{{ this.heading }} <span v-if="!entry">({{ products.length }})</span></h1>
      <ul v-if="!entry">
        <li v-for="element in products" :key="element.id">
          <!-- Pass down every product in the category into separate Information components -->
          <Information :product="element" />
        </li>
      </ul>
      <div v-else class="entry">
        <p>
          This is a web application where you can browse product information from an Imaginary Clothing Brands warehouse!
        </p>
        <p>
          Press any of the above buttons to search products from that category. Product information is loaded from
          <a href="https://bad-api-assignment.reaktor.com/" target="_blank">https://bad-api-assignment.reaktor.com/</a>.
        </p>
        <p>
          Source code can be seen by clicking the button in the right upper corner or
          <a href="https://github.com/Mahamurahti/Reaktor-Assignment-2021" target="_blank">here</a>.
        </p>
        <p>
          Made by <a href="https://erickeranen.muuta.net/" target="_blank">Eric Keränen</a>
        </p>
      </div>
      <div v-if="loading" class="loading">
        <img src="../assets/loading.svg"
             alt="Loading image">
      </div>
      <img @click="scrollToTop"
           class="scroll"
           src="../assets/arrow.svg"
           alt="Picture of an arrow"
           title="Scroll to top">
    </div>
  </div>
</template>

<script>
import Navigation from "@/components/Navigation";
import Information from "@/components/Information";

export default {
  name: 'Home',
  components: {
    Navigation,
    Information,
  },
  data() {
    return {
      // Store all the products and pass them into separate Information components
      products: Array,
      heading: 'Welcome!',
      loading: false,
      entry: true,
    }
  },
  methods: {
    // Grab the product information passed down from Navigation
    printProduct(emit) {
      this.products = JSON.parse(emit.contents);
      this.entry = false;
    },
    // Display loading screen
    loadingScreen(emit){ this.loading = emit; },
    // Update Heading of the page
    updateHead(emit){ this.heading = emit; },
    // Load the data of the "Entry page"
    loadEntry(emit){
      this.entry = emit;
      this.heading = 'Welcome!';
    },
    // Scroll to the top of the site instantly
    scrollToTop(){ document.documentElement.scrollTop = 0; }
  }
}
</script>

<style scoped>
.home{
  min-height: 100vh;
  margin: auto;
  max-width: 900px;

  padding: 10px;
}
h1{
  color: white;
  font-size: 42px;
  padding: 40px 0;

  text-align: left;
}
p{
  text-align: left;
  color: white;
  font-size: 22px;
  margin-bottom: 40px;
}
a:link{
  color: orange;
}
a:visited{
  color: orangered;
}
li{
  position: relative;

  list-style-type: none;
  text-align: left;
  padding: 10px;
  margin-bottom: 10px;

  border: 2px solid #910024;
}
.loading{
  position: fixed;
  top: 0;
  left: 0;

  display: flex;
  justify-content: center;
  align-items: center;

  width: 100%;
  height: 100%;

  background-color: rgba(47,47,47,0.80);
}
.loading img{
  height: 200px;
  width: 200px;

  animation: loading 2s linear infinite;
}
.scroll{
  position: fixed;
  bottom: 40px;
  right: 40px;

  width: 60px;
  height: 60px;

  padding: 10px;

  transform: rotate(270deg);
  border-radius: 50%;

  transition: .2s ease-in-out;
}
@media (max-width: 880px) {
  .scroll{
    bottom: 20px;
    right: 20px;

    width: 30px;
    height: 30px;

    padding: 5px;
  }
}
.scroll:hover{
  transform: scale(1.2) rotate(270deg);
  background-color: rgba(101,101,101,1);
}
@keyframes loading {
  to{
    transform: rotate(360deg);
  }
}
</style>
