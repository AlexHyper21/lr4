<template>
  <header class="header">
    <div class="header__inner">
      <img :src="logo" alt="пиксельмаркет" width="168" height="32" />
      <div class="header__cart">
        <img :src="cartIcon" alt="" width="24" height="24" />
        <span>Корзина</span>
        <span v-if="cartCount > 0" class="header__badge">{{ cartCount }}</span>
      </div>
    </div>
  </header>

  <main class="page">
    <section class="page__catalog">
      <h1 class="page__title">Каталог цифровых товаров</h1>
      <ProductList :products="products" @add-to-cart="addToCart" />
    </section>
    <aside class="page__cart">
      <ShoppingCart :items="cartItems" @remove="removeFromCart" @clear="clearCart" />
    </aside>
  </main>
</template>

<script>
import ProductList from './components/ProductList.vue'
import ShoppingCart from './components/ShoppingCart.vue'
import logo from './assets/logo.svg'
import cartIcon from './assets/cart.svg'
import product1 from './assets/product-1.webp'
import product2 from './assets/product-2.webp'
import product3 from './assets/product-3.webp'
import product4 from './assets/product-4.webp'

export default {
  name: 'App',
  components: {
    ProductList,
    ShoppingCart
  },
  data() {
    return {
      logo,
      cartIcon,
      products: [
        { id: 1, name: 'Набор иконок «Контур» · 640 штук', seller: 'Студия Кегль', price: 29, oldPrice: 45, rating: 4.8, reviews: 127, formats: ['SVG', 'FIGMA', 'PNG'], imageUrl: product1, isNew: false },
        { id: 2, name: 'Шрифт «Гротеск Норд» · 4 начертания', seller: 'Типобюро Север', price: 59, oldPrice: null, rating: 4.6, reviews: 84, formats: ['OTF', 'WOFF2'], imageUrl: product2, isNew: true },
        { id: 3, name: 'UI-кит «Пульт» для дашбордов', seller: 'Студия Кегль', price: 89, oldPrice: 120, rating: 4.9, reviews: 212, formats: ['FIGMA'], imageUrl: product3, isNew: false },
        { id: 4, name: 'Мокапы смартфонов · 24 сцены', seller: 'Фото Лаб', price: 35, oldPrice: null, rating: 4.3, reviews: 56, formats: ['PSD', 'PNG'], imageUrl: product4, isNew: false }
      ],
      cartItems: []
    }
  },
  computed: {
    cartCount() {
      return this.cartItems.reduce((sum, item) => sum + item.quantity, 0)
    }
  },
  methods: {
    addToCart(payload) {
      const existing = this.cartItems.find((item) => item.id === payload.product.id)
      if (existing) {
        existing.quantity += payload.quantity
      } else {
        this.cartItems.push({
          id: payload.product.id,
          name: payload.product.name,
          price: payload.product.price,
          imageUrl: payload.product.imageUrl,
          quantity: payload.quantity
        })
      }
    },
    removeFromCart(id) {
      this.cartItems = this.cartItems.filter((item) => item.id !== id)
    },
    clearCart() {
      this.cartItems = []
    }
  }
}
</script>

<style scoped>
.header {
  background: var(--color-surface);
  border-bottom: 1px solid var(--color-border);
}

.header__inner {
  max-width: 1280px;
  margin: 0 auto;
  padding: 14px 24px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.header__cart {
  position: relative;
  display: flex;
  align-items: center;
  gap: 8px;
  font-size: 14px;
  font-weight: 500;
}

.header__badge {
  min-width: 22px;
  height: 22px;
  padding: 0 6px;
  border-radius: 11px;
  background: var(--color-accent);
  color: #fff;
  font-size: 12px;
  font-weight: 600;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.page {
  max-width: 1280px;
  margin: 0 auto;
  padding: 32px 24px 48px;
  display: grid;
  grid-template-columns: 1fr 340px;
  gap: 28px;
  align-items: start;
}

.page__title {
  margin: 0 0 20px;
  font-size: 28px;
  font-weight: 700;
}

.page__cart {
  position: sticky;
  top: 24px;
}

@media (max-width: 960px) {
  .page {
    grid-template-columns: 1fr;
  }

  .page__cart {
    position: static;
  }
}
</style>
