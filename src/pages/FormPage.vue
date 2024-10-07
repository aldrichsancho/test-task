<template>
  <q-page padding>
    <q-card>
      <q-card-section>
        <h6>Form Submission</h6>
      </q-card-section>
      <q-card-section>
        <BaseForm />
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
import BaseForm from '../components/BaseForm.vue';
export default {
  components: {
    BaseForm,
  },
};
</script>
