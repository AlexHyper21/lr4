# ЛР 4 — пиксельмаркет на Vue.js

Интернет-магазин цифровых товаров (вариант 3) на Vue 3 (Options API) и Vite.

Компоненты:

- `ProductCard.vue` — карточка товара, кнопка «Добавить в корзину» генерирует событие `add-to-cart` с данными о товаре;
- `ProductList.vue` — список карточек (`v-for`), пробрасывает событие родителю;
- `ShoppingCart.vue` — содержимое корзины, итоговая сумма.

Массив `cartItems` хранится в родительском компоненте `App.vue` и пополняется по событию `add-to-cart`.

## Запуск

```bash
npm install
npm run dev
```

Приложение откроется по адресу http://localhost:5173

## Сборка

```bash
npm run build
npm run preview
```
