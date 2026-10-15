<template>
  <section class="cart">
    <h2 class="cart__title">Корзина</h2>
    <p v-if="items.length === 0" class="cart__empty">Корзина пуста. Добавьте товары из каталога.</p>
    <template v-else>
      <ul class="cart__list">
        <li v-for="item in items" :key="item.id" class="cart__item">
          <img :src="item.imageUrl" :alt="item.name" width="56" height="40" />
          <div class="cart__info">
            <span class="cart__name">{{ item.name }}</span>
            <span class="cart__meta">{{ item.quantity }} × {{ item.price }} BYN</span>
          </div>
          <button class="cart__remove" type="button" :aria-label="'Удалить ' + item.name" @click="$emit('remove', item.id)">×</button>
        </li>
      </ul>
      <div class="cart__total">
        <span>Итого</span>
        <strong>{{ total }} BYN</strong>
      </div>
      <button class="cart__clear" type="button" @click="$emit('clear')">Очистить корзину</button>
    </template>
  </section>
</template>

<script>
export default {
  name: 'ShoppingCart',
  props: {
    items: {
      type: Array,
      required: true
    }
  },
  emits: ['remove', 'clear'],
  computed: {
    total() {
      return this.items.reduce((sum, item) => sum + item.price * item.quantity, 0)
    }
  }
}
</script>

<style scoped>
.cart {
  padding: 20px;
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-card);
}

.cart__title {
  margin: 0 0 16px;
  font-size: 20px;
}

.cart__empty {
  margin: 0;
  color: var(--color-muted);
  font-size: 14px;
}

.cart__list {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.cart__item {
  display: flex;
  align-items: center;
  gap: 10px;
}

.cart__item img {
  border-radius: 6px;
  object-fit: cover;
}

.cart__info {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: 2px;
}

.cart__name {
  font-size: 13px;
  font-weight: 600;
}

.cart__meta {
  font-size: 12px;
  color: var(--color-muted);
}

.cart__remove {
  width: 28px;
  height: 28px;
  border: none;
  border-radius: 6px;
  background: var(--color-bg);
  font-size: 18px;
  cursor: pointer;
}

.cart__total {
  display: flex;
  justify-content: space-between;
  align-items: baseline;
  margin: 18px 0 12px;
  padding-top: 14px;
  border-top: 1px solid var(--color-border);
  font-size: 15px;
}

.cart__total strong {
  font-size: 22px;
}

.cart__clear {
  width: 100%;
  height: 40px;
  border: 1px solid var(--color-border);
  border-radius: var(--radius-control);
  background: none;
  font: inherit;
  font-size: 14px;
  cursor: pointer;
}
</style>
