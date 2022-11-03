<script setup lang="ts">
  import { reactive } from "vue";

  interface IProps {
    email?: string;
    password?: string;
  }

  const props = withDefaults(defineProps<IProps>(), {
    email: "student001@jedlik.eu",
    password: "student001",
  });

  interface IReactiveData {
    email: string;
    password: string;
  }

  const r = reactive<IReactiveData>({
    email: props.email,
    password: props.password,
  });
</script>

<template>
  <q-dialog>
    <q-card>
      <q-card-section>
        <div class="text-h6">Login</div>
      </q-card-section>
      <q-card-section>
        <q-input
          v-model="r.email"
          filled
          label="E-mail:"
          :rules="[(v) => (v != null && v != '') || 'Please fill in!']"
          type="text"
        />
        <q-input
          v-model="r.password"
          filled
          label="Password:"
          :rules="[(v) => (v != null && v != '') || 'Please fill in!']"
          type="text"
        />
      </q-card-section>
      <q-card-actions align="right">
        <q-btn color="primary" flat label="Cancel" />
        <q-btn color="primary" label="Login" />
      </q-card-actions>
    </q-card>
  </q-dialog>
</template>

<style lang="scss" scoped></style>
