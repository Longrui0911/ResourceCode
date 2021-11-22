<template>
  <div class="add-resources">
    <form @submit.prevent="submitResources()">
      <div class="add-resources__form-control">
        <label for="title">Title</label>
        <input type="text" id="title" name="title" ref="titleInput" />
      </div>
      <div class="add-resources__form-control">
        <label for="description">Description</label>
        <textarea
          type="text"
          id="description"
          name="description"
          ref="descriptionInput"
          rows="3"
        />
      </div>
      <div class="add-resources__form-control">
        <label for="link">Link</label>
        <input type="url" id="link" name="link" ref="linkInput" />
      </div>
      <div>
        <button type="submit">Add resources</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "AddResources",
  inject: ["addResources"],
  methods: {
    submitResources() {
      const title = this.$refs.titleInput.value;
      const description = this.$refs.descriptionInput.value;
      const link = this.$refs.linkInput.value;
      this.addResources(title.trim(), description.trim(), link.trim());
    },
  },
};
</script>

<style scoped>
.add-resources {
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
  margin: 2rem auto;
  max-width: 40rem;
}
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
}
.add-resources__form-control {
  margin: 1rem 0;
}
</style>