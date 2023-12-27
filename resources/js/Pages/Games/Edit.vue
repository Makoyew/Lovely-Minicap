<script setup>
import { ref } from 'vue';
import { router } from '@inertiajs/vue3';
import NewLayout from '@/Layouts/NewLayout.vue';
import Navbar from '@/Components/Navbar.vue';
import { Link } from '@inertiajs/vue3';

const props = defineProps({
  game: Object,
  attributes: Object
});

const form = ref({
  ...props.game.data,
  attribute_id: props.game.data.attribute_id,
  image: null
});

const updateGame = () => {
  router.post(`/games/${props.game.data.id}`, form.value, {
    preserveState: true,
  });
};

const handleImageChange = (event) => {
  if (event.target.files.length > 0) {
    form.value.image = event.target.files[0];
  }
};
</script>

<template>
  <NewLayout>
    <Navbar />
    <div class="banner">
      <img src="https://www.epicgardening.com/wp-content/uploads/2023/09/North-Carolina-perennial-flower-garden-in-full-sun.jpg" alt="Banner Image" />
      <div class="banner-overlay"></div>
      <div class="banner-content">
        <div class="banner-title">Edit Plant</div>
        <div class="banner-subtitle">Modify the details of your plant</div>
      </div>
    </div>
    <div class="form-container">
      <div class="flex justify-end">
        <Link :href="route('games.index')" :active="route().current('games.index')">
          <i class="fa-solid fa-circle-chevron-left"></i>
          <span :hidden="hidden"> Back</span>
        </Link>
      </div>
      <h1>Edit Plant</h1>
      <div class="form-content">
        <form @submit.prevent="updateGame">
          <div class="form-group">
            <label for="name">Name</label>
            <input type="text" id="name" v-model="form.name" required>
          </div>
          <div class="form-group">
            <label for="attribute_id">Plant Type</label>
            <select id="attribute_id" v-model="form.attribute_id" required>
              <option value="" disabled>Select a plant type</option>
              <option v-for="attribute in props.attributes.data" :key="attribute.id" :value="attribute.id">{{ attribute.name }}</option>
            </select>
          </div>
          <div class="form-group">
            <label for="description">Description</label>
            <textarea id="description" v-model="form.description" required rows="2"></textarea>
          </div>
          <div class="form-group">
            <label for="image">Image</label>
            <input type="file" id="image" @change="handleImageChange">
          </div>
          <div class="form-group">
            <label for="release_date">Release Date</label>
            <input type="date" id="release_date" v-model="form.release_date" required>
          </div>
          <div class="flex justify-end form-group">
            <button type="submit">Update Plant</button>
          </div>
        </form>
      </div>
    </div>
  </NewLayout>
</template>

<style scoped>
.banner {
  position: relative;
  height: 300px;
  overflow: hidden;
}

.banner img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.banner-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(to bottom, rgba(0, 0, 0, 0.6) 0%, rgba(0, 0, 0, 0) 50%);
}

.banner-content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  color: #fff;
}

.banner-title {
  font-size: 36px;
  font-weight: bold;
  margin-bottom: 10px;
}

.banner-subtitle {
  font-size: 18px;
}

.form-container {
  max-width: 500px;
  margin: 0 auto;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  margin-top: 20px;
  margin-bottom: 20px;
}

.form-container h1 {
  padding: 20px;
  background-color: #007bff;
  color: #fff;
  font-size: 24px;
  font-weight: bold;
  text-align: center;
  margin: 0;
}

.form-content {
  padding: 20px;
}

.form-group {
  margin-bottom: 16px;
}

.form-group label {
  display: block;
  font-size: 14px;
  margin-bottom: 8px;
  color: #333;
}

.form-group input,
.form-group select,
.form-group textarea {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 14px;
}

.form-group button {
  background-color: #007bff;
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
  font-weight: bold;
}

.form-group button:hover {
  background-color: #0056b3;
}
</style>
