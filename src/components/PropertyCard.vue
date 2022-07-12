<template>
  <router-link :to="{ name: 'Property', params: { id: property.id } }">
    <img :src="property.image_url" :alt="property.title" />
    <h3>
      {{ property.title }}
    </h3>
    <p>Area: {{ property.area }}</p>
  </router-link>
</template>

<script>
export default {
  props: ["property"],
};
</script>

<style></style>
