<template>
  <div id="nav">
    <h1 @click="loadEntryContent">Imaginary Clothing Brand</h1>
    <div class="links">
      <button @click="getGloves">Gloves</button>
      <button @click="getBeanies">Beanies</button>
      <button @click="getFacemasks">Facemasks</button>
      <button @click="toSourceCode" v-on:mouseenter="showArrow()" v-on:mouseleave="hideArrow()">
        <span v-if="!onHover">Source Code</span>
        <img v-else src="../assets/arrow.svg" alt="Picture of an arrow">
      </button>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Navigation",
  data() {
    return {
      onHover: false
    }
  },
  methods: {
    // It would lessen code quite much if the emits were in one functions, that every async function calls,
    // but for some reason it doesn't work and Home component displays an error every time...

    // Get the data of gloves from the api
    async getGloves() {
      this.$emit('product:load', true);
      let url = 'https://api.allorigins.win/get?url=https://bad-api-assignment.reaktor.com/v2/products/gloves';
      await axios.get(url)
          .then(data => {
            // Update main page with correct data
            this.$emit('product:call', data.data)
            this.$emit('product:head', 'Gloves')
            this.$emit('product:load', false);
          })
          .catch(err => {
            // Display the error message on the main page
            console.error(err)
            this.$emit('product:call', '')
            this.$emit('product:head', err)
            this.$emit('product:load', false);
          })
    },
    // Get the data of beanies from the api
    async getBeanies() {
      this.$emit('product:load', true);
      let url = 'https://api.allorigins.win/get?url=https://bad-api-assignment.reaktor.com/v2/products/beanies';
      await axios.get(url)
          .then(data => {
            // Update main page with correct data
            this.$emit('product:call', data.data)
            this.$emit('product:head', 'Beanies')
            this.$emit('product:load', false);
          })
          .catch(err => {
            // Display the error message on the main page
            console.error(err)
            this.$emit('product:call', '')
            this.$emit('product:head', err)
            this.$emit('product:load', false);
          })
    },
    // Get the data of facemasks from the api
    async getFacemasks() {
      this.$emit('product:load', true);
      let url = 'https://api.allorigins.win/get?url=https://bad-api-assignment.reaktor.com/v2/products/facemasks';
      await axios.get(url)
          .then(data => {
            // Update main page with correct data
            this.$emit('product:call', data.data)
            this.$emit('product:head', 'Facemasks')
            this.$emit('product:load', false);
          })
          .catch(err => {
            // Display the error message on the main page
            console.error(err)
            this.$emit('product:call', '')
            this.$emit('product:head', err)
            this.$emit('product:load', false);
          })
    },
    // LOad the content of the 'Entry page'
    loadEntryContent(){ this.$emit('content:entry', true) },
    // Open source code on GitHub
    toSourceCode(){
      window.open('https://github.com/Mahamurahti/Reaktor-Assignment-2021', '_blank');
    },
    showArrow(){ this.onHover = true; },
    hideArrow() { this.onHover = false; }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Lobster&display=swap');
#nav {
  display: flex;
  align-items: center;

  min-height: 10vh;

  background-color: #910024;
  color: white;
}

#nav h1{
  font-family: 'Lobster', cursive, Avenir, Helvetica, Arial, sans-serif;
  font-weight: lighter;
  font-size: 42px;

  height: 150px;
  width: 25vw;

  margin-right: 20px;

  border-bottom: 2px solid transparent;

  display: flex;
  justify-content: center;
  align-items: center;

  transition: .2s ease-in-out;
}

#nav h1:hover{
  cursor: pointer;
  border-bottom: 2px solid white;
}

.links{
  display: flex;
  width: 75vw;
}

#nav button{
  font-family: 'Lobster', cursive;

  width: 180px;
  height: 150px;

  margin-right: 20px;

  font-size: 24px;

  display: flex;
  justify-content: center;
  align-items: center;

  font-weight: lighter;
  text-decoration: none;

  background-color: transparent;
  color: white;

  border: none;
  border-bottom: 2px solid transparent;
  outline: none;

  transition: .2s ease-in-out;

}

#nav button:hover{
  cursor: pointer;
  border-bottom: 2px solid white;
}

#nav button:last-child{
  margin-left: auto;
}

#nav button img{
  width: 60px;
  height: 60px;
}
@media (max-width: 880px) {
  #nav{
    flex-direction: column;
  }
  #nav h1{
    width: 350px;
    margin-right: 0;
  }
  .links{
    flex-direction: column;
    width: revert;
  }
  #nav button{
    margin-right: 0;
    margin-bottom: 20px;
    height: 40px;
  }
  #nav button:last-child{
    margin-left: 0;
  }
}
</style>