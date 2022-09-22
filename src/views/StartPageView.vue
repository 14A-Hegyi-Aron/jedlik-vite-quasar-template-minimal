<script setup lang="ts">
  let osztaly = ref("A");
  const state = reactive({
    evfolyam: 14,
    gombSzine: "primary",
    text: "Jedlik",
  });

  function osztaly_valtoztato() {
    if (osztaly.value == "A") {
      osztaly.value = "F";
      state.gombSzine = "deep-orange";
    } else {
      osztaly.value = "A";
      state.gombSzine = "primary";
    }
  }

  function evfolyam_valtoztato() {
    if (state.evfolyam == 14) {
      state.evfolyam = 12;
      state.gombSzine = "deep-orange";
    } else {
      state.evfolyam = 14;
      state.gombSzine = "primary";
    }
  }
</script>

<template>
  <q-page>
    <h1>Osztály: {{ state.evfolyam }}.{{ osztaly }}</h1>
    <q-btn
      class="q-ma-xs"
      :color="state.gombSzine"
      label="Osztály váltó"
      no-caps
      @:click="osztaly_valtoztato()"
    />
    <q-btn
      class="q-ma-xs"
      :color="state.gombSzine"
      label="Évfolyam váltó"
      no-caps
      @:click="evfolyam_valtoztato()"
    />
    <q-input
      v-model="state.text"
      clearable
      hint="Írj be valamit"
      label="Standard"
      loading
      :rules="[(val) => val.length <= 3 || 'Max 3 karakter']"
    />
    <h1>{{ state.text }}</h1>
  </q-page>
</template>

<style lang="scss" scoped></style>
