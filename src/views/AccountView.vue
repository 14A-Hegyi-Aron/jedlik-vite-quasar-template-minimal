<script setup lang="ts">
  import { computed, reactive } from "vue";
  import { useUsersStore } from "../store/usersStore";

  const usersStore = useUsersStore();

  interface IReactiveData {
    showDialog: boolean;
  }

  const r = reactive<IReactiveData>({
    showDialog: false,
  });
  const anyLoggedUser = computed(() => (usersStore.getLoggedUser ? true : false));
</script>

<template>
  <q-page>
    <div class="row window-height flex-center justify-evenly">
      <q-btn
        class="shadow-10"
        color="info"
        :label="anyLoggedUser ? 'Show logout dialog' : 'Show login dialog'"
        no-caps
        @click="r.showDialog = true"
      />
      <q-btn
        class="shadow-10"
        color="blue"
        :label="anyLoggedUser ? 'Logout from Google' : 'Login with Google'"
        no-caps
      />
      <login-dialog
        v-model:show="r.showDialog"
        email="vmi@vmi.eu"
        password="vmi"
        :show-dialog="r.showDialog"
        @close-login-dialog="r.showDialog = false"
      />
    </div>
  </q-page>
</template>

<style lang="scss" scoped></style>
