<template>
  <base-dialog v-if="inputIsInvalid" title="Invalid Input">
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>Please check all inputs</p>
    </template>
    <template #actions>
      <base-button @click="confirmError">Okey</base-button>
    </template>
  </base-dialog>
  <base-card>
    <form @submit.prevent="submitData">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" id="title" ref="titleInput" />
      </div>

      <div class="form-control">
        <label for="description">Description</label>
        <textarea id="description" rows="3" ref="desInput"></textarea>
      </div>

      <div class="form-control">
        <label for="link">Link</label>
        <input type="url" id="link" ref="linkInput" />
      </div>
      <div>
        <base-button type="submit">Add Resource</base-button>
      </div>
    </form>
  </base-card>
</template>

<script>
import BaseButton from './UI/BaseButton.vue';
import BaseDialog from './UI/BaseDialog.vue';
export default {
  components: { BaseDialog, BaseButton },
  inputIsInvalid: false,
  inject: ['theResource'],
  methods: {
    submitData() {
      const enteredTitle = this.$refs.titleInput.value;
      const enteredDescription = this.$refs.desInput.value;
      const enteredUrl = this.$refs.linkInput.value;

      if (
        enteredTitle.trim() === '' ||
        enteredDescription.trim() === '' ||
        enteredUrl.trim() === ''
      ) {
        this.inputIsInvalid = true;
        // return;
        // alert('Invalid Input');
        return;
      }

      this.theResource(enteredTitle, enteredDescription, enteredUrl);
    },
    confirmError() {
      this.inputIsInvalid = false;
    },
  },
};
</script>

<style scoped>
label {
  font-weight: bold;
  display: block;
  margin-bottom: 0.5rem;
}

input,
textarea {
  display: block;
  width: 100%;
  font: inherit;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus,
textarea:focus {
  outline: none;
  border-color: #3a0061;
  background-color: #f7ebff;
}

.form-control {
  margin: 1rem 0;
}
</style>
