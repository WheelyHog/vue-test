<script>
import {defineComponent} from "vue";

export default defineComponent({
  name: 'CatalogView'
})

</script>

<template>
  <div class="products-list">
    <div
        class="product"
        v-for="product in store.products"
        :key="product.id"
        @click="goToProductPage(product.id)"
    >
      <img :src="product.thumbnail" alt="">
      <h2>Brand: {{ product.brand }}</h2>
      <p>Description: {{ product.description }}</p>
      <p>Price: ${{ product.price }}</p>
    </div>
  </div>
</template>

<style scoped>
.products-list {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}

.product {
  flex-basis: 28%;
  margin: 8px;
  padding: 16px;
  box-shadow: 0 0 14px 1px #e6e6e6;
  cursor: pointer;
}

.product img {
  width: 70%;
}
</style>

<script setup>
import {onMounted} from "vue";
import {productsStore} from "@/stores/products";
import router from "@/router";

const store = productsStore()


const goToProductPage = (id) => {
  router.push({name: 'ProductView', params: {id}})
}


onMounted(() => {
  store.fetchProductsFromDB()
})
</script>