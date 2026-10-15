<template>
  <article class="card">
    <div class="card__image">
      <img :src="product.imageUrl" :alt="product.name" width="320" height="220" />
      <span v-if="product.oldPrice" class="card__badge card__badge--sale">−{{ discount }} %</span>
      <span v-else-if="product.isNew" class="card__badge card__badge--new">Новинка</span>
    </div>
    <div class="card__body">
      <div class="card__tags">
        <span v-for="format in product.formats" :key="format" class="card__tag">{{ format }}</span>
      </div>
      <h3 class="card__title">{{ product.name }}</h3>
      <p class="card__seller">{{ product.seller }}</p>
      <div class="card__rating">
        <img v-for="n in 5" :key="n" :src="n <= Math.round(product.rating) ? starIcon : starEmptyIcon" alt="" width="14" height="14" />
        <span class="card__rating-text">{{ product.rating }} · {{ product.reviews }} отзывов</span>
      </div>
      <div class="card__price">
        <span class="card__price-current">{{ product.price }} BYN</span>
        <span v-if="product.oldPrice" class="card__price-old">{{ product.oldPrice }} BYN</span>
      </div>
      <div class="card__actions">
        <label class="card__qty">
          <span>Кол-во</span>
          <input v-model.number="quantity" type="number" min="1" max="99" />
        </label>
        <button class="card__button" type="button" :disabled="quantity < 1" @click="addToCart">
          Добавить в корзину
        </button>
      </div>
    </div>
  </article>
</template>

<script>
import starIcon from '../assets/star.svg'
import starEmptyIcon from '../assets/star-empty.svg'

export default {
  name: 'ProductCard',
  props: {
    product: {
      type: Object,
      required: true
    }
  },
  emits: ['add-to-cart'],
  data() {
    return {
      quantity: 1,
      starIcon,
      starEmptyIcon
    }
  },
  computed: {
    discount() {
      return Math.round((1 - this.product.price / this.product.oldPrice) * 100)
    }
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart', {
        product: this.product,
        quantity: this.quantity
      })
      this.quantity = 1
    }
  }
}
</script>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-card);
  overflow: hidden;
}

.card__image {
  position: relative;
  aspect-ratio: 320 / 220;
  background: var(--color-bg);
}

.card__image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.card__badge {
  position: absolute;
  top: 10px;
  left: 10px;
  padding: 3px 8px;
  border-radius: 6px;
  font-size: 12px;
  font-weight: 600;
  color: #fff;
}

.card__badge--sale {
  background: #c8371a;
}

.card__badge--new {
  background: var(--color-text);
}

.card__body {
  display: flex;
  flex-direction: column;
  gap: 8px;
  padding: 14px 16px 16px;
  flex: 1;
}

.card__tags {
  display: flex;
  gap: 6px;
}

.card__tag {
  padding: 2px 7px;
  border-radius: 5px;
  background: var(--color-bg);
  font-size: 11px;
  font-weight: 600;
  color: var(--color-muted);
}

.card__title {
  margin: 0;
  font-size: 15px;
  font-weight: 600;
  line-height: 1.35;
}

.card__seller {
  margin: 0;
  font-size: 13px;
  color: var(--color-muted);
}

.card__rating {
  display: flex;
  align-items: center;
  gap: 2px;
}

.card__rating-text {
  margin-left: 6px;
  font-size: 12px;
  color: var(--color-muted);
}

.card__price {
  display: flex;
  align-items: baseline;
  gap: 8px;
  margin-top: auto;
}

.card__price-current {
  font-size: 22px;
  font-weight: 700;
}

.card__price-old {
  font-size: 13px;
  color: var(--color-muted);
  text-decoration: line-through;
}

.card__actions {
  display: flex;
  gap: 8px;
  align-items: flex-end;
}

.card__qty {
  display: flex;
  flex-direction: column;
  gap: 2px;
  font-size: 11px;
  color: var(--color-muted);
}

.card__qty input {
  width: 56px;
  height: 40px;
  padding: 0 8px;
  border: 1px solid var(--color-border);
  border-radius: var(--radius-control);
  font: inherit;
  font-size: 15px;
  color: var(--color-text);
}

.card__button {
  flex: 1;
  height: 40px;
  border: none;
  border-radius: var(--radius-control);
  background: var(--color-accent);
  color: #fff;
  font: inherit;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
}

.card__button:hover {
  background: #b83a17;
}

.card__button:disabled {
  background: var(--color-border);
  color: var(--color-muted);
  cursor: not-allowed;
}
</style>
