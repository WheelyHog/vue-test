<script>
import {defineComponent} from "vue";

export default defineComponent({
  name: 'ProductDetails'
})
</script>

<template>
  <button @click="router.push({name: 'Catalog'})">Back to Catalog</button>
  <div class="product">
    <div class="product-image">
      <img :src="selectedProduct.thumbnail" alt="">
    </div>
    <div class="product-details">
      <p>Brand: {{ selectedProduct.brand }}</p>
      <p>Description: {{ selectedProduct.description }}</p>
      <h2>Price: {{ selectedProduct.price }}</h2>
      <button @click="addToCart">Add to cart</button>
    </div>
  </div>
</template>

<style scoped>

</style>

<script setup>
import {computed} from "vue";
import {useRoute, useRouter} from "vue-router";
import {productsStore} from "@/stores/products";

const route = useRoute()
const store = productsStore()
const router = useRouter()

const selectedProduct = computed(() => {
  return store.products.find((item) => item.id === Number(route.params.id))
})

const addToCart = () => {
  store.addToCart(selectedProduct.value)
  router.push({name: 'CartView'})
}
</script>