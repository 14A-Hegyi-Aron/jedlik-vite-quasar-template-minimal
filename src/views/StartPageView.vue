<script setup lang="ts">
  import { IShopItem } from "src/types";
  import ShopItem from "src/components/ShopItem.vue";
  import ShopCart from "src/components/ShopCart.vue";

  const items: Array<IShopItem> = reactive([
    { id: 201, name: "Alma", price: 12, imageSrc: "src/assets/alma.jpg" },
    { id: 202, name: "Banán", price: 24, imageSrc: "src/assets/banán.jpg" },
    { id: 203, name: "Barack", price: 36, imageSrc: "src/assets/barack.jpg" },
    { id: 204, name: "Citrom", price: 48, imageSrc: "src/assets/citrom.jpg" },
    { id: 205, name: "Eper", price: 60, imageSrc: "src/assets/eper.jpg" },
    { id: 206, name: "Kivi", price: 72, imageSrc: "src/assets/kivi.jpg" },
    { id: 207, name: "Málna", price: 84, imageSrc: "src/assets/málna.jpg" },
    { id: 208, name: "Narancs", price: 96, imageSrc: "src/assets/narancs.jpg" },
    { id: 209, name: "Szamóca", price: 108, imageSrc: "src/assets/szamóca.jpg" },
  ]);

  let cart: Array<IShopItem> = reactive([]);
  let total = ref(0);

  function updateCart(e: IShopItem) {
    cart.push(e);
    total.value += e.price;
  }

  function emptyCart() {
    cart.splice(0);
    total.value = 0;
  }
</script>

<template>
  <q-page>
    <shop-cart :cart="cart" :total="total" @empty-cart="emptyCart()" />
    <div class="row">
      <div v-for="item in items" :key="item.id" class="col-xs-12 col-sm6 col-md-4 col-lg-3">
        <shop-item :item="item" style="mix-blend-mode: luminosity" @update-cart="updateCart" />
      </div>
    </div>
  </q-page>
</template>

<style scoped lang="scss"></style>
