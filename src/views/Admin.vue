<template>
  <div v-if="properties">
    <input type="text" v-model="search" placeholder="Search..." />
    <select v-model="area">
      <option value="All" selected>All</option>
      <option value="Durban">Durban</option>
      <option value="Cape Town">Cape Town</option>
      <option value="Pretoria">Pretoria</option>
    </select>
    <table>
      <thead>
        <tr>
          <th>ID</th>
          <th>Image Preview</th>
          <th>Title</th>
          <th>Area</th>
          <th>Bedrooms</th>
          <th @click="sortPrice">Price</th>
          <th>Image URL</th>
          <th><button>Add</button></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="property of properties" :key="property.id">
          <td>{{ property.id }}</td>
          <td><img :src="property.image_url" :alt="property.title" /></td>
          <td>{{ property.title }}</td>
          <td>{{ property.area }}</td>
          <td>{{ property.bedrooms }}</td>
          <td>R{{ property.price }}</td>
          <td>{{ property.image_url }}</td>
          <td>
            <button @click="deleteProperty(property.id)">Delete</button>
            <UpdateModal :property="property" />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import UpdateModal from "../components/UpdateModal.vue";
export default {
  data() {
    return {
      search: "",
      area: "All",
    };
  },
  computed: {
    properties() {
      return this.$store.state.properties?.filter((property) => {
        let isMatch = true;
        if (!property.title.toLowerCase().includes(this.search.toLowerCase()))
          isMatch = false;
        if (this.area !== "All" && property.area !== this.area) isMatch = false;
        return isMatch;
      });
    },
  },
  mounted() {
    this.$store.dispatch("getProperties");
  },
  components: { UpdateModal },
  methods: {
    deleteProperty(id) {
      this.$store.dispatch("deleteProperty", id);
    },
    sortPrice() {
      this.$store.commit("sortPropertiesByPrice");
    },
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
