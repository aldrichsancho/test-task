<template>
  <form @submit.prevent="submitForm">
    <div class="row" style="padding-bottom: 14px">
      <div class="col-12 col-sm-6" style="padding-bottom: 8px">
        <FormKit
          type="text"
          label="Name"
          name="name"
          v-model="formData.name"
          validation="required"
        />
      </div>
      <div class="col-12 col-sm-6">
        <FormKit
          type="email"
          label="Email"
          name="email"
          v-model="formData.email"
          validation="required|email"
        />
      </div>
    </div>

    <button
      type="submit"
      :disabled="!isFormValid"
      class="btn btn-primary col-12 col-md-6"
    >
      Save
    </button>
  </form>
</template>

<script setup>
import { ref, computed } from 'vue';

const formData = ref({
  name: '',
  email: '',
});

const isFormValid = computed(() => formData.value.name && formData.value.email);

const submitForm = () => {
  if (!isFormValid.value) {
    console.log('Form is invalid');
    return;
  }

  const jsonOutput = JSON.stringify(formData.value);
  console.log('Data:', jsonOutput);
  // Call API for saving data
};
</script>
