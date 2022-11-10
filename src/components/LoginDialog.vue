<script setup lang="ts">
  import { useUsersStore } from "src/store/usersStore";
  import { computed, reactive } from "vue";

  interface IProps {
    email?: string;
    password?: string;
    showDialog: boolean;
  }

  const props = withDefaults(defineProps<IProps>(), {
    email: "student001@jedlik.eu",
    password: "student001",
    showDialog: true,
  });

  // eslint-disable-next-line no-unused-vars
  const emit = defineEmits<{ (e: "close-login-dialog"): void }>();

  interface IReactiveData {
    email: string;
    password: string;
  }

  const r = reactive<IReactiveData>({
    email: props.email,
    password: props.password,
  });

  const usersStore = useUsersStore();
  const anyLoggedUser = computed(() => (usersStore.getLoggedUser ? true : false));

  function LoginLogout() {
    if (anyLoggedUser.value) {
      usersStore.logOut();
    } else {
      usersStore.loginUser({ email: r.email, password: r.password });
    }
  }
</script>

<template>
  <q-dialog v-model="$props.showDialog" transition-hide="rotate" transition-show="rotate">
    <q-card class="q-pa-md" style="width: 100%">
      <q-form>
        <q-card-section>
          <div class="text-h6">Login</div>
        </q-card-section>
        <q-card-section>
          <q-input
            v-model="r.email"
            :disable="anyLoggedUser"
            filled
            label="E-mail:"
            :rules="[(v) => (v != null && v != '') || 'Please fill in!']"
            type="text"
          />
        </q-card-section>
        <q-card-section v-if="!anyLoggedUser">
          <q-input
            v-model="r.password"
            filled
            label="Password:"
            :rules="[(v) => (v != null && v != '') || 'Please fill in!']"
            type="password"
          />
        </q-card-section>
        <q-card-actions align="center">
          <q-btn
            class="q-mr-md"
            color="green"
            :label="anyLoggedUser ? 'Logout' : 'Login'"
            no-caps
            @click="LoginLogout()"
          />
          <q-btn color="red" flat label="Cancel" no-caps @click="emit('close-login-dialog')" />
        </q-card-actions>
      </q-form>
    </q-card>
  </q-dialog>
</template>

<style lang="scss" scoped></style>
