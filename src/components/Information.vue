<template>
  <div class="info">
    <div class="head">
      <h1>{{ product.name }}</h1>
      <div class="stock">
        <Search :element="product" />
      </div>
    </div>
    <h2>
      {{ product.price }}€ |
      Manufactuer: {{ product.manufacturer }} |
      Colors: {{ product.color.toString() }}
    </h2>
  </div>
</template>

<script>
import Search from "@/components/Search";

export default {
  name: "Information",
  components: {
    Search
  },
  props: {
    // This is the product the Home component passes in the v-for loop which
    // will be further passed down for the Search component
    product: Object
  }
}
</script>

<style scoped>
.head{
  display: flex;
  width: 100%;
  color: white;
}
.stock{
  display: block;
  text-align: right;
  margin-left: auto;

  transition: .2s ease-in-out;
}
h2{
  font-weight: lighter;
  color: white;
}
</style>