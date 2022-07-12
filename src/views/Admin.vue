<template>
  <div v-if="properties">
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Image Preview</th>
          <th>Title</th>
          <th>Area</th>
          <th>Bedrooms</th>
          <th>Image URL</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="property of properties" :key="property.id">
          <td>{{ property.id }}</td>
          <td><img :src="property.image_url" :alt="property.title" /></td>
          <td>{{ property.title }}</td>
          <td>{{ property.area }}</td>
          <td>{{ property.bedrooms }}</td>
          <td>{{ property.image_url }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  computed: {
    properties() {
      return this.$store.state.properties;
    },
  },
  mounted() {
    this.$store.dispatch("getProperties");
  },
};
</script>

<style>
table img {
  height: 100px;
  aspect-ratio: 1;
  object-fit: cover;
}
</style>
