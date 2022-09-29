<script setup lang="ts">
  import { IShopItem } from "src/types";
  import { PropType } from "vue";
  defineProps({
    item: {
      type: Object as PropType<IShopItem>,
      required: true,
    },
  });

  const emmit = defineEmits<{
    // eslint-disable-next-line no-unused-vars
    (event: "update-cart", value: IShopItem): void;
  }>();

  function addToCart(item: IShopItem) {
    emmit("update-cart", item);
  }
</script>

<template>
  <q-card class="q-ma-md shadow-6">
    <q-img :alt="item.name" :src="item.imageSrc">
      <div class="text-subtitle2 bg-blue absolute-top text-center text-bold">
        {{ item.name }} - {{ item.price }} Ft
      </div>
    </q-img>
    <q-card-actions class="absolute-bottom">
      <q-btn
        class="full-width shadow-6"
        color="primary"
        label="Add to Cart"
        no-caps
        @click="addToCart(item)"
      />
    </q-card-actions>
  </q-card>
</template>

<style lang="scss" scoped></style>
