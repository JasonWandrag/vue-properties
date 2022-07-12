<template>
  <div v-if="properties" class="flex-container">
    <PropertyCard
      v-for="property of properties"
      :key="property.id"
      :property="property"
    />
  </div>
  <div v-else>Loading...</div>
</template>
<script>
import PropertyCard from "../components/PropertyCard.vue";
export default {
  mounted() {
    this.$store.dispatch("getProperties");
  },
  computed: {
    properties() {
      return this.$store.state.properties;
    },
  },
  components: { PropertyCard },
};
</script>
<style>
.flex-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 20px;
}
</style>
