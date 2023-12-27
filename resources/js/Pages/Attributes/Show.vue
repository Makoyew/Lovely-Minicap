<script setup>
  import { defineProps, computed } from 'vue';
  import NewLayout from '@/Layouts/NewLayout.vue';
  import Navbar from '@/Components/Navbar.vue';
  import { Link } from '@inertiajs/vue3';


  const props = defineProps({
    attribute: Object,
    games: Object,
  });

  const getImageUrl = (game) => {
  return game.image.startsWith('http') ? game.image : `/storage/${game.image}`;
};

  const attributeGames = computed(() => {
  if (props.games.data.length > 0) {
    console.log('Attribute details from the first game object:', props.games.data[0].attribute);
  }

  const filteredGames = props.games.data.filter((game) => {
    console.log('Current game attribute ID:', game.attribute?.id);

    const isAttributeMatch = game.attribute?.id === props.attribute.data.id;
    if (!isAttributeMatch) {
      console.log(`Attribute ID mismatch: ${game.attribute?.id} !== ${props.attribute.data.id}`);
    }
    return isAttributeMatch;
  });

  console.log('Filtered games:', filteredGames);
  return filteredGames;
});


  const formatDate = (dateString) => {
    if (!dateString) return 'Unknown date'; // Handle null, undefined, or empty strings
    const options = { year: 'numeric', month: 'long', day: 'numeric' };
    const date = new Date(dateString);
    return isNaN(date) ? 'Invalid date' : date.toLocaleDateString(undefined, options);
  };

  console.log('attribute:', props.attribute);
  console.log('Games:', props.games);
  </script>


<style scoped>
.banner {
  position: relative;
  height: 400px;
  overflow: hidden;
}

.banner img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  position: absolute;
  top: 0;
  left: 0;
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
  margin-bottom: 20px;
}

/* Game List */
.game-list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
  padding: 20px;
}

/* Game Card Styles */
.game-card {
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 5px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  overflow: hidden;
  transition: transform 0.2s;
  max-width: 300px;
  display: flex;
  flex-direction: column;
}

.game-card:hover {
  transform: translateY(-5px);
}

.game-image {
  overflow: hidden;
  height: 200px;
  text-align: center;
  display: flex;
  justify-content: center;
}

.fixed-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.game-details {
  padding: 15px;
  text-align: left;
}

.game-title {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 10px;
  text-align: center; /* Center the title */
}

.info-item {
  margin-bottom: 5px;
}

.info-label {
  font-weight: bold;
}

.info-value {
  color: #555;
}

.game-description {
  font-size: 14px;
  color: #777;
  margin-top: 10px;
}
</style>

<template>
  <NewLayout>
    <Navbar />

    <div class="banner">
      <img src="https://images.pexels.com/photos/158028/bellingrath-gardens-alabama-landscape-scenic-158028.jpeg?cs=srgb&dl=pexels-pixabay-158028.jpg&fm=jpg" alt="Banner Image" />
      <div class="banner-overlay"></div>
      <div class="banner-content">
        <div class="banner-title">Explore Beautiful Plants</div>
        <div class="banner-subtitle">Discover a world of green wonders</div>
      </div>
    </div>

    <!-- Game List Section -->
    <div class="game-list">
      <!-- Back Button -->
      <div class="back-button-container">
        <Link :href="route('attributes.index')" :active="route().current('attributes.index')">
          <i class="fa-solid fa-circle-chevron-left"></i>
          <span :hidden="hidden"> Back</span>
        </Link>
      </div>

      <!-- Game Cards -->
      <div class="game-card" v-for="game in attributeGames" :key="game.id" @click="viewDetails(game.id)">
        <div class="game-image">
          <img :src="getImageUrl(game)" alt="Game Cover" class="fixed-image">
        </div>
        <div class="game-details">
          <h2 class="game-title">{{ game.name }}</h2>
          <div class="info-item">
            <span class="info-label">Plant Type: </span>
            <span class="info-value">{{ game.attribute.name }}</span>
          </div>
          <div class="info-item">
            <span class="info-label">Release Date: </span>
            <span class="info-value">{{ formatDate(game.release_date) }}</span>
          </div>
          <p class="game-description">{{ game.description }}</p>
        </div>
      </div>
    </div>
  </NewLayout>
</template>
