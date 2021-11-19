<template>
  <div class="container">
    <div class="card">
      <h1>Register now</h1>
      <BaseForm @submitForm="showAlert = true" />
      <BaseNotification
        :show="showAlert"
        @close="showAlert = false"
        message="Form validated"
      />
    </div>
  </div>
</template>

<script>
import BaseForm from "./BaseForm.vue";
import BaseNotification from "./BaseNotification.vue";

export default {
  name: "FormValidation",
  components: {
    BaseForm,
    BaseNotification,
  },
  data() {
    return {
      showAlert: false,
    };
  },
};
</script>
