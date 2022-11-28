<template>
  <div>
    <FormKit
      type="form"
      :actions="false"
      submit-label="submit"
      @submit="handleSubmit"
    >
    </FormKit>
    <FormKit
      label="email"
      name="email"
      type="email"
      validation="required|(500)asyncValidation"
      validation-visibility="dirty"
      :validation-rules="{ asyncValidation }"
      :validation-messages="{
        asyncValidation: asyncValidationError,
      }"
    ></FormKit>
  </div>
</template>
<script setup lang="ts">
const asyncValidationError = ref('');
const submitPending = ref(false);
const asyncValidation = async () => {
  await new Promise((r) => {
    setTimeout(() => r(), 1000);
  });
  asyncValidationError.value = 'Bad email !';
  return false;
};

const handleSubmit = () => {
  console.log('form submit.');
};
</script>
