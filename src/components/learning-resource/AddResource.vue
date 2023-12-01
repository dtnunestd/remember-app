<template>
  <BaseDialog v-if="modalOpen" title="Invalid input" @close="closeModal">
    <template #default>
      <p>Unfortunately, at least one input value is invalid.</p>
      <p>
        Please check all inputs and make sure you enter at least a few
        characters into each input field.
      </p>
    </template>
    <template v-slot:actions>
      <BaseButton @click="closeModal">Okay</BaseButton>
    </template>
  </BaseDialog>
  <BaseCard>
    <form @submit.prevent="handleSubmit">
      <div class="form-control">
        <label for="title">Title</label>
        <input type="text" id="title" name="title" v-model="title" />
      </div>
      <div class="form-control">
        <label for="link">Description</label>
        <textarea
          id="description"
          name="description"
          rows="3"
          v-model="description"
        />
      </div>
      <div class="form-control">
        <label for="link">Link</label>
        <input type="text" id="link" name="link" v-model="link" />
      </div>
      <div>
        <BaseButton type="submit">Add Resource</BaseButton>
      </div>
    </form>
  </BaseCard>
</template>

<script>
export default {
  data() {
    return {
      title: '',
      description: '',
      link: '',
      modalOpen: false,
    };
  },
  inject: ['addResource'],
  methods: {
    handleSubmit() {
      if (
        this.title.trim() === '' ||
        this.description.trim() === '' ||
        this.link.trim() === ''
      ) {
        this.modalOpen = true;
        return;
      }
      const resource = {
        id: new Date().toISOString(),
        title: this.title,
        description: this.description,
        link: this.link,
      };
      this.modalOpen = false;
      this.addResource(resource);
    },
    closeModal() {
      this.modalOpen = false;
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
