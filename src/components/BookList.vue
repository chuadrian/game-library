<template>
  <div class="book-list">
    <div v-for="book in books" :key="book.id" class="book-item">
      <img :src="book.image" :alt="book.title" @click="showDetails(book)" />
      <h3>{{ book.title }}</h3>
      <p>{{ book.author }}</p>
      <span
        class="heart-icon"
        :class="{ favorited: book.favourited }"
        @click="toggleFavorite(book)"
      >
        <i :class="book.favourited ? 'fas fa-heart' : 'far fa-heart'"></i>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    books: {
      type: Array,
      required: true,
    },
  },
  methods: {
    toggleFavorite(book) {
      this.$emit('favourite-toggle', book);
    },
    showDetails(book) {
      this.$emit('show-details', book);
    },
  },
};
</script>
  
  
<style scoped>
  .book-list{
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    margin: 0 auto;
  }
  .book-item {
    background-color: #1e1e2f;
    border-radius: 8px;
    padding: 10px;
    text-align: center;
    margin-bottom: 16px;
    margin-top: 18px;
  }
  .book-item img {
    width: 100%;
    height: auto;
    max-height: 200px; 
    object-fit: cover; 
    border-radius: 8px;
  }

  .heart-icon.favorited {
    color: #00d4ff;
  }
  .book-item h3 {
    margin: 10px 0 5px;
    font-size: 1.2em;
  }

  .book-item p {
    margin: 5px 0;
  }

  .book-item .heart-icon {
    color: red;
    text-shadow: 0 0 10px rgba(255, 38, 0, 0.7);
    cursor: pointer;
  }

  
  @media (max-width: 400px) {
    .book-list {
      grid-template-columns: 1fr;
      width: 80%;
    }
  }

  
  @media (max-width: 768px) {
    .book-list {
      grid-template-columns: repeat(2, 1fr);
      gap: 15px;
    }
    .book-item {
      margin-bottom: 12px;
      margin-top: 12px;
    }
  }

  @media (max-width: 480px) {
    .book-list {
      justify-content: center;
      grid-template-columns: 1fr;
      gap: 10px;
      align-items: center;
    }
    .book-item {
      margin-bottom: 8px;
      margin-top: 8px;
    }
    .book-item img {
      max-height: 150px;
    }
  }

  @media (max-width: 320px) {
    .book-list {
      gap: 5px;
    }
    .book-item {
      margin-bottom: 5px;
      margin-top: 5px;
    }
    .book-item img {
      max-height: 100px;
    }
  }
</style>
