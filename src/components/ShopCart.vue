<script setup lang="ts">
  import { IShopItem } from "src/types";
  import { PropType } from "vue";

  const props = defineProps({
    cart: {
      type: Object as PropType<IShopItem[]>,
      required: true,
    },
    total: {
      type: Number,
      required: true,
      default: 0,
    },
  });

  const emmit = defineEmits(["empty-cart"]);

  function emptyCart() {
    emmit("empty-cart");
  }
</script>

<template>
  <q-card class="bg-info">
    <q-card-actions>
      <p>Cart component: {{ cart.length }} items</p>
      <q-space />
      <q-btn class="negative" color="primary" no-caps @click="emptyCart()">Empty cart</q-btn>
    </q-card-actions>
    <q-card-section>
      <div v-for="item in cart" :key="item.id">
        <p>{{ item.name }} - {{ item.price }} Ft</p>
      </div>
      <p>Total: {{ total }} Ft</p>
    </q-card-section>
  </q-card>
</template>

<style lang="scss" scoped></style>
