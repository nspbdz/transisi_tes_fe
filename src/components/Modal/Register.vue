<template>
  <BaseDialog ref="refModalRegister">
    <section class="register pa-5 mt-5">
      <h1 class="text-center">Register</h1>
      <v-form v-model="valid" @submit.prevent="handleSubmit">
        <v-text-field v-model="formValues.email" label="Email" required></v-text-field>
        <v-text-field v-model="formValues.password" label="Password" required></v-text-field>
        <div class="d-flex justify-center">
          <v-btn type="submit" color="primary">Register</v-btn>
        </div>
      </v-form>
    </section>
  </BaseDialog>
</template>
<script setup>
import BaseDialog from "@/components/Base/Dialog.vue";
import { reactive } from "@vue/reactivity";
import { useAuthStore } from "../../stores/auth";
import { useRouter } from "vue-router";

const authStore = useAuthStore();
const router = useRouter();

const formValues = reactive({
  email: "eve.holt@reqres.in",
  password: "pistol",
});

const handleSubmit = async () => {
  authStore.register(formValues).then(async () => {
    await router.push("/admin");
  });
};
</script>