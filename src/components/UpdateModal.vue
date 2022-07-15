<template>
  <button @click="toggleModal">Update</button>
  <div v-if="active" class="modal">
    <button @click="toggleModal">x</button>
    <form @submit.prevent="updateProperty">
      <input type="text" v-model="property.title" />
      <select v-model="property.area">
        <option value="All" selected>All</option>
        <option value="Durban">Durban</option>
        <option value="Cape Town">Cape Town</option>
        <option value="Pretoria">Pretoria</option>
      </select>
      <input type="text" v-model="property.image_url" />
      <input type="number" v-model="property.bedrooms" />
      <input type="number" v-model="property.price" />
      <button type="submit">Update</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ["property"],
  data() {
    return {
      active: false,
    };
  },
  methods: {
    toggleModal() {
      this.active = !this.active;
    },
    updateProperty() {
      this.$store.dispatch("updateProperty", this.property);
      this.toggleModal();
    },
  },
};
</script>

<style>
.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: white;
  padding: 30px;
  border: 5px solid black;
}
</style>
