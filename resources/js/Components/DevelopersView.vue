<script setup>
import { defineProps } from 'vue';
import { router } from '@inertiajs/vue3';

const props = defineProps({
  attributes: Object,
  attribute: Object,
});

const viewDetails = (attributeId) => {
  router.visit(route('attributes.show', { attribute: attributeId }));
};
</script>

<style scoped>
/* New styles for the banner */
.banner {
  background-image: url('https://cutewallpaper.org/35/flower-garden-background-wallpaper/2981123749.jpg');
  background-size: cover;
  background-position: center;
  color: #fff;
  text-align: center;
  padding: 100px 20px;
}

/* Existing styles */
.attribute-list {
  display: flex;
  justify-content: center;
  gap: 20px;
  padding: 20px;
}

.attribute-card {
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 5px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  overflow: hidden;
  transition: transform 0.2s;
  max-width: 300px;
}

.attribute-card:hover {
  transform: translateY(-5px);
}

.attribute-image {
  overflow: hidden;
}

.attribute-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
}

.attribute-details {
  padding: 15px;
  text-align: center;
}

.attribute-name {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 10px;
}

.w-full {
  width: 100%;
}

.h-48 {
  height: 12rem;
}

.object-cover {
  object-fit: cover;
}

.rounded-t-xl {
  border-top-left-radius: 0.5rem;
  border-top-right-radius: 0.5rem;
}
</style>

<template>
  <div>
    <!-- Cool banner on top -->
    <div class="banner">
      <h1>Plant Types</h1>
      <p>Discover our amazing collection of attributes</p>
    </div>

    <!-- List of attributes -->
    <div class="attribute-list">
      <div class="attribute-card" v-for="attribute in attributes.data" :key="attribute.id">
        <div class="attribute-image" @click="viewDetails(attribute.id)">
          <img :src="attribute.image" alt="attribute Image" class="object-cover w-full h-48 rounded-t-xl">
        </div>
        <div class="attribute-details">
          <h3 class="attribute-name">{{ attribute.name }}</h3>
        </div>
      </div>
    </div>
  </div>
</template>
