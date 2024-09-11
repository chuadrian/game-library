<template>
  <div class="favorites">
    <h2>Your Favorites</h2>
    <div v-if="favorites.length === 0" class="no-favorites">
      You haven't added any favorites yet.
    </div>
    <div v-else class="favorites-list">
      <div v-for="book in favorites" :key="book.id" class="favorite-item">
        <img :src="book.image" :alt="book.title" class="favorite-image">
        <div class="favorite-details">
          <h3>{{ book.title }}</h3>
          <p>{{ book.author }}</p>
          <button @click="$emit('remove-favorite', book)" class="remove-button">
            Remove from Favorites
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    favorites: {
      type: Array,
      required: true
    }
  }
}
</script>

<style scoped>
.favorites {
  margin-top: 40px;
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 10px;
  padding: 20px;
}

.favorites h2 {
  color: #000;
  margin-bottom: 20px;
}

.no-favorites {
  color: #ccc;
  font-style: italic;
}

.favorites-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
}

.favorite-item {
  background-color: rgba(255, 255, 255, 0.2);
  border-radius: 8px;
  overflow: hidden;
  transition: transform 0.3s ease;
}

.favorite-item:hover {
  transform: translateY(-5px);
}

.favorite-image {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.favorite-details {
  padding: 15px;
}

.favorite-details h3 {
  color: #3498db;
  margin: 0 0 10px 0;
}

.favorite-details p {
  color: #ccc;
  margin: 0 0 15px 0;
}

.remove-button {
  background-color: #ff4757;
  color: white;
  border: none;
  padding: 8px 12px;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.remove-button:hover {
  background-color: #ff6b81;
}
</style>