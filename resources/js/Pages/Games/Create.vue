<script setup>
import NewLayout from '@/Layouts/NewLayout.vue';
import Navbar from '@/Components/Navbar.vue';
import { useForm } from '@inertiajs/vue3';
import { usePage, useRoute } from '@inertiajs/inertia-vue3';
import { Link } from '@inertiajs/vue3';


const props = defineProps({
  attributes: Object
});

const form = useForm({
    name: '',
    attribute_id: '',
    description: '',
    image: null,
    release_date: '',
});

function submit() {
    form.post(route('games.store'), {
        onSuccess: () => {
            useRoute().push({ name: 'games.index' });
            usePage().props.flash.success = 'Game created successfully.';
        },
        onError: error => {
        }
    });
}

function handleImageChange(event) {
    form.image = event.target.files[0];
}

console.log(props.attributes.data);
</script>

<style scoped>
.back-button-container {
  position: absolute;
  top: 10px;
  right: 10px;
  z-index: 999;
}

.back-button-container Link {
  background-color: #007bff;
  color: #fff;
  padding: 8px 12px;
  border-radius: 4px;
  cursor: pointer;
  display: flex;
  align-items: center;
}

.back-button-container Link:hover {
  background-color: #0056b3;
}

.back-button-container Link i {
  margin-right: 5px;
}
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

/* Form Container */
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

<template>
  <NewLayout>
    <Navbar />

    <!-- Banner Section -->
    <div class="banner">
      <img src="https://hips.hearstapps.com/hmg-prod/images/perennial-flowers-and-plants-1674072475.jpeg?crop=1.00xw:0.752xh;0,0&resize=1200:*" alt="Banner Image" />
      <div class="banner-overlay"></div>
      <div class="banner-content">
        <div class="banner-title">Add New Plant</div>
        <div class="banner-subtitle">Fill in the details and let your plant shine</div>
      </div>
    </div>

    <!-- Form Container -->
    <div class="form-container">
        <div class="flex justify-end">
        <Link :href="route('games.index')" :active="route().current('games.index')">
                <i class="fa-solid fa-circle-chevron-left"></i>
                <span :hidden="hidden"> Back</span>
            </Link>
      </div>
      <h1>Add New Plant</h1>
      <div class="form-content">
        <form @submit.prevent="submit">
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
            <button type="submit">Add Plant</button>
          </div>
        </form>
      </div>
    </div>
  </NewLayout>
</template>
