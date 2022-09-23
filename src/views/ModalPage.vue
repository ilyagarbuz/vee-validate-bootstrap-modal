<template>
  <div class="container">
    <button @click="isOpen = true" class="btn btn-success">
      <i class="bi bi-pencil"></i>
    </button>

    <ModalBase :open="isOpen" @close="isOpen = !isOpen">
      <form @submit.prevent="submit">
        <div class="mb-3">
          <label for="email" class="form-label">Email address</label>
          <input @change="email" type="text" class="form-control" id="email" />
          <div class="invalid-feedback">{{ errors.email }}</div>
        </div>
        <div class="mb-3">
          <label for="password" class="form-label">Password</label>
          <input
            @change="password"
            type="password"
            class="form-control"
            id="password"
          />
          <div class="invalid-feedback">{{ errors.password }}</div>
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
    </ModalBase>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { useField, useForm } from "vee-validate";
import { string, object } from "yup";
import ModalBase from "@/components/ModalBase.vue";

const isOpen = ref(false);

const validationSchema = object({
  email: string().required().email(),
  password: string().required().min(8),
});

const { handleSubmit, errors } = useForm({
  validationSchema,
});

const { handleChange: email } = useField("email");
const { handleChange: password } = useField("password");

const submit = handleSubmit((values) => {
  console.log(values);
  isOpen.value = false;
});
</script>
