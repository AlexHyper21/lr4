<template>
  <div class="product-list">
    <ProductCard
      v-for="product in products"
      :key="product.id"
      :product="product"
      @add-to-cart="onAddToCart"
    />
  </div>
</template>

<script>
import ProductCard from './ProductCard.vue'

export default {
  name: 'ProductList',
  components: {
    ProductCard
  },
  props: {
    products: {
      type: Array,
      required: true
    }
  },
  emits: ['add-to-cart'],
  methods: {
    onAddToCart(payload) {
      this.$emit('add-to-cart', payload)
    }
  }
}
</script>

<style scoped>
.product-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
}
</style>
