<template>
  <div class="container">
    <router-link :to="{ name: 'modal-test' }">Modal page</router-link>
    <form @submit.prevent="submit" class="w-50 mx-auto mt-5">
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
      <label class="form-label" for="age"> Are you 18 ? </label>
      <div class="mb-3 d-flex gap-5">
        <div class="form-check">
          <input
            v-model="age"
            class="form-check-input"
            type="radio"
            name="age"
            id="yes"
            value="yes"
          />
          <label class="form-check-label" for="yes"> Yes </label>
        </div>
        <div class="form-check">
          <input
            v-model="age"
            class="form-check-input"
            type="radio"
            name="age"
            id="no"
            value="no"
          />
          <label class="form-check-label" for="no"> No </label>
        </div>
      </div>
      <div v-if="age === 'yes'" class="mb-3 form-check">
        <input
          v-model="check"
          type="checkbox"
          class="form-check-input"
          id="check"
          checked
          disabled
        />
        <label class="form-check-label" for="check">Check me out</label>
        <div class="invalid-feedback">{{ errors.check }}</div>
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script setup>
import { useForm, useField } from "vee-validate";
import { object, string } from "yup";

const validations = object({
  email: string().required().email(),
  password: string().required("This is required field").min(6),
  age: undefined,
  check: undefined,
});

const { handleSubmit, errors } = useForm({
  validationSchema: validations,
  initialValues: {
    age: "no",
    check: true,
  },
});

const { handleChange: email } = useField("email");
const { handleChange: password } = useField("password");
const { value: age } = useField("age");
const { value: check } = useField("check");

const submit = handleSubmit((values) => {
  console.log(values);
});
</script>

<style>
.invalid-feedback {
  display: block !important;
}
</style>
