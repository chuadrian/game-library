<template>
  <div class="container">
    <header class="header">
      <h1>Library</h1>
      <button class="signup-button" @click="showSignup = true">Log in / Sign Up</button>
    </header>

    <!-- Search Component -->
    <SearchBar v-model="searchQuery" />

    <!-- Book List Component -->
    <BookList
      :books="paginatedBooks"
      @favourite-toggle="toggleFavorite"
      @show-details="showBookDetails"
    />

    <!-- Pagination Component -->
    <PageList
      :current-page="currentPage"
      :total-pages="totalPages"
      @page-changed="handlePageChange"
    />

    <!-- Book Details Modal -->
    <BookDetails
      v-if="showDetails"
      :book="selectedBook"
      @close-details="closeBookDetails"
    />

    <!-- Favourites List -->
    <FavoritesList
      :favorites="favorites"
      @remove-favorite="removeFromFavorites"
    />

    <!--SignUP Page-->
    <SignupPage 
      v-if="showSignup"
      @close="showSignup = false" />
  </div>
</template>

<script>
import SearchBar from './components/SearchBar.vue';
import BookList from './components/BookList.vue';
import PageList from './components/PageList.vue';
import BookDetails from './components/BookDetails.vue';
import FavoritesList from './components/FavoritesList.vue';
import SignupPage from './components/SignupPage.vue'

export default {
  components: {
    SearchBar,
    BookList,
    PageList,
    BookDetails,
    FavoritesList,
    SignupPage,
  },

  /**
   * The data function returns an object that contains the data for the component.
   * 
   * The data object contains the following properties:
   * - books: An array of objects, each representing a book.
   * - searchQuery: A string that contains the search query.
   * - favorites: An array of objects, each representing a book that has been favorited.
   * - currentPage: A number that represents the current page.
   * - booksPerPage: A number that represents the number of books per page.
   * - selectedBook: An object that represents the book that is currently selected.
   * - showDetails: A boolean that indicates whether the book details should be shown.
   * - showAddBook: A boolean that indicates whether the add book form should be shown.
   * - showSignup: A boolean that indicates whether the signup page should be shown.
   */


  /**
   * The data function returns an object that contains the data for the component.
   * 
   * The data object contains the following properties:
   * - books: An array of objects, each representing a book.
   * - searchQuery: A string that contains the search query.
   * - favorites: An array of objects, each representing a book that has been favorited.
   * - currentPage: A number that represents the current page.
   * - booksPerPage: A number that represents the number of books per page.
   * - selectedBook: An object that represents the book that is currently selected.
   * - showDetails: A boolean that indicates whether the book details should be shown.
   * - showAddBook: A boolean that indicates whether the add book form should be shown.
   * - showSignup: A boolean that indicates whether the signup page should be shown.
   */

  data() {
    return {
      books: [
        {id: 1, title: 'Call Of Duty', author: '$28.78', image: 'https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/1938090/ss_c107f0b2214eaa85d504c819a6b3fbbf9bf4c2e5.600x338.jpg?t=1725901837', description: 'Description 1', favourited: false},
        {id: 2, title: 'Minecraft', author: '$37.09', image: 'https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/1672970/ss_73b488e696e3ae45f5d0a5750de524c231dab8a2.600x338.jpg?t=1717003107', description: 'Description 2', favourited: false},
        {id: 3, title: 'Greedfall', author: '$12.90', image: 'https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/606880/ss_559dff7041b638b596c78fd26275320cd95efc71.600x338.jpg?t=1712313669', description: 'Description 3', favourited: false},
        {id: 4, title: 'Visions Of Mana', author: '$56.00', image: 'https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/2490990/ss_23ad17020248542c7ca57e9e655e28890e868c11.600x338.jpg?t=1725269328', description: 'Description 4', favourited: false},
        {id: 5, title: 'Black Skylands', author: '$53.22', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/1143810/header.jpg?t=1725355896', description: 'Description 5', favourited: false},
        {id: 6, title: 'Arc Survival Ascended', author: '$45.21', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/2399830/header.jpg?t=1726014607', description: 'Description 6', favourited: false},
        {id: 7, title: 'Ghost Recon', author: '$5.00', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/2231380/header.jpg?t=1697654010', description: 'Description 7', favourited: false},
        {id: 8, title: 'Darkest Dungeon', author: '$21.00', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/1940340/1ffe7f6d0223110870ba7a498c3f4713686b4a34/hero_capsule.jpg?t=1724367449', description: 'Description 8', favourited: false},
        {id: 9, title: 'Balatro', author: '$12.00', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/2379780/hero_capsule.jpg?t=1725631254', description: 'Description 9', favourited: false},
        {id: 10, title: 'Cult Of The Lab', author: '$5.00', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/1313140/header_alt_assets_6.jpg?t=1724977430', description: 'Description 10', favourited: false},
        {id: 11, title: 'Risk Of Rain 2', author: '$12.00', image: '	https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/632360/header.jpg?t=1724778884', description: 'Description 1', favourited: false},
        {id: 12, title: 'Hades', author: '$5.00', image: '	https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/1145350/header.jpg?t=1723829198', description: 'Description 2', favourited: false},
        {id: 13, title: 'Lockdown Protocol', author: '$52.00', image: 'https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/2780980/header_292x136.jpg?t=1721725451', description: 'Description 3', favourited: false},
        {id: 14, title: 'Rainbows X Seige', author: '$32.00', image: 'https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/359550/header_292x136.jpg?t=1719504498', description: 'Description 4', favourited: false},
        {id: 15, title: 'Fallout 4 VR', author: '$22.00', image: 'https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/611660/header_292x136.jpg?t=1607445202', description: 'Description 5', favourited: false},
        {id: 16, title: 'Once Human', author: '$24.00', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/2139460/61d997964e0261a57025b4af9034a3c885e48aa9/hero_capsule.jpg?t=1723792749', description: 'Description 6', favourited: false},
        {id: 17, title: 'Destiny 2', author: '$5.00', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/1085660/hero_capsule.jpg?t=1720218333', description: 'Description 7', favourited: false},
        {id: 18, title: 'Banana', author: '$12.00', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/2923300/hero_capsule.jpg?t=1724181871', description: 'Description 8', favourited: false},
        {id: 19, title: 'PUBG BattleGrounds', author: '$2.00', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/578080/05b3dd28f609db8dbbdbb3ce6ccac089249fd181/hero_capsule.jpg?t=1725501407', description: 'Description 9', favourited: false},
        {id: 20, title: 'DOTA 2', author: '$52.00', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/570/hero_capsule.jpg?t=1724428927', description: 'Description 10', favourited: false},
        {id: 21, title: 'Spectre Divide', author: '$12.00', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/2641470/5f5e885724d28d94a21d6a8efbe35af93a4e21a3/hero_capsule.jpg?t=1726083901', description: 'Description 1', favourited: false},
        {id: 22, title: 'The First Descendant', author: '$52.00', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/2074920/1a69eaa872d63e77af3aa969e4bb0729e7c0c73d/hero_capsule.jpg?t=1725356337', description: 'Description 2', favourited: false},
        {id: 23, title: 'FIFA 25', author: '$72.00', image: 'https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/2669320/ss_bab390c4ca80ca91d5984440cec2eea12b4848ba.600x338.jpg?t=1724359060', description: 'Description 3',  favourited: false},
        {id: 25, title: 'Monster Hunter Rise', author: '$62.00', image: 'https://shared.akamai.steamstatic.com//store_item_assets/steam/apps/1446780/hero_capsule.jpg?t=1715075183', description: 'Description 5', favourited: false},
        {id: 26, title: 'NARUTO X BORUTO Ultimate Ninja STORM CONNECTIONS', author: '$54.87', image: 'https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/1020790/ss_726a0954289660537a03f058ffa44aa42a199edc.600x338.jpg?t=1721858461', description: 'Description 6', favourited: false},
        {id: 27, title: 'ONE PIECE: PIRATE WARRIORS 4', author: '$52.00', image: 'https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/1089090/ss_47cfb549dc12ac02bbf39af5b4bfdc516275a065.600x338.jpg?t=1718095269', description: 'Description 7', favourited: false},
        {id: 28, title: 'Black Myth: Wukong', author: '$22.00', image: 'https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/2358720/ss_d9391ab31a4d15dddf7ba4949bfa44f5d9170580.600x338.jpg?t=1725007201', description: 'Description 8', favourited: false},
        {id: 29, title: 'Baldur Gate 3', author: '$32.00', image: 'https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/1086940/ss_c73bc54415178c07fef85f54ee26621728c77504.600x338.jpg?t=1725654125', description: 'Description 9', favourited: false},
        {id: 30, title: 'Satisfactory 1.0', author: '$42.40', image: 'https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/526870/ss_306f1c5828e3afeccea89f1d1f0e3f954a042bd7.600x338.jpg?t=1726051378', description: 'Description 10', favourited: false},
      ],

      searchQuery: '',
      favorites: [],
      currentPage: 1,
      booksPerPage: 6,
      selectedBook: null,
      showDetails: false,
      showAddBook: false,
      showSignup: false
    };
  },
  computed: {

    /**
     * Returns a filtered list of books, where the title of each book contains
     * the search query.
     * @returns {Array} An array of books that match the search query.
     */

    filteredBooks() {
      return this.books.filter((book) =>
        book.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      );

    },

    /**
     * Returns a subset of filteredBooks, limited to the number of books per
     * page. The subset is determined by the currentPage.
     * @returns {Array} An array of books that match the search query, limited
     * to the number of books per page.
     */

    paginatedBooks() {
      const start = (this.currentPage - 1) * this.booksPerPage;
      return this.filteredBooks.slice(start, start + this.booksPerPage);

    },
    totalPages() {
      return Math.ceil(this.filteredBooks.length / this.booksPerPage);
    },
  },
  methods: {
    toggleFavorite(book) {
      book.favourited = !book.favourited;
      if (book.favourited) {
        this.favorites.push(book);
      } else {
        this.favorites = this.favorites.filter((fav) => fav.id !== book.id);
      }
      this.saveFavorites();
    },
    handlePageChange(newPage) {
      this.currentPage = newPage;
    },
    showBookDetails(book) {
      this.selectedBook = book;
      this.showDetails = true;
    },
    closeBookDetails() {
      this.showDetails = false;
      this.selectedBook = null;
    },
    removeFromFavorites(book) {
      book.favourited = false;
      this.favorites = this.favorites.filter((fav) => fav.id !== book.id);
      this.saveFavorites();
    },
    saveFavorites() {
      localStorage.setItem('favorites', JSON.stringify(this.favorites));
    },
    loadFavorites() {
      const savedFavorites = localStorage.getItem('favorites');
      if (savedFavorites) {
        this.favorites = JSON.parse(savedFavorites);
        this.favorites.forEach(favorite => {
          const book = this.books.find(b => b.id === favorite.id);
          if (book) {
            book.favourited = true;
          }
        });
      }
    },
  },
  created() {
    this.loadFavorites();
  },
};
</script>

<style>
:root {
  --primary-color: #00ffcc;
  --secondary-color: #00d4ff;
  --accent-color: #1e1e2f;
  --text-color: #ecf0f1;
  --background-color: #1e1e2f;
}

body {
  margin: 0;
  padding: 0;
  font-family: 'Orbitron', Arial, sans-serif;
  background-color: var(--background-color);
  color: var(--text-color);
}

#app {
  min-height: 100vh;
  background-color: var(--background-color);
  display: flex;
  justify-content: center;
  align-items: flex-start;
  padding-top: 2rem;
}


.container {
  width: 90%;
  max-width: 1200px;
  padding: 2rem;
  background-color: rgba(30, 30, 47, 0.8);
  box-shadow: 0 4px 20px rgba(0, 255, 204, 0.3);
  border-radius: 8px;
  border: 2px solid var(--primary-color);
}


.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.signup-button {
  padding: 10px 20px;
  font-size: 16px;
  background: linear-gradient(90deg, var(--primary-color), var(--secondary-color));
  color: var(--accent-color);
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-family: 'Orbitron', sans-serif;
  text-transform: uppercase;
}

.signup-button:hover {
  box-shadow: 0 0 15px rgba(0, 255, 204, 0.7);
  transform: scale(1.05);
}


h1 {
  color: var(--primary-color);
  font-size: 2.5rem;
  margin-bottom: 1.5rem;
  text-align: center;
  text-transform: uppercase;
}

h2 {
  color: var(--secondary-color);
  font-size: 1.8rem;
  margin-bottom: 1rem;
}

.book-list, .favorites-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 2rem;
}

.book-item, .favorite-item {
  background-color: rgba(45, 45, 74, 0.8);
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 255, 204, 0.2);
  overflow: hidden;
  transition: all 0.3s ease;
  border: 1px solid var(--primary-color);
}

.book-item:hover, .favorite-item:hover {
  transform: translateY(-5px) scale(1.03);
  box-shadow: 0 4px 20px rgba(0, 255, 204, 0.4);
}

.book-item img, .favorite-item img {
  width: 100%;
  height: 250px;
  object-fit: cover;
  border-bottom: 2px solid var(--primary-color);
}

.book-item h3, .favorite-item h3 {
  color: var(--primary-color);
  margin: 0.5rem 0;
  font-size: 1.2rem;
}

.book-item p, .favorite-item p {
  color: var(--text-color);
  margin: 0.5rem 0;
  font-size: 0.9rem;
}

.heart-icon {
  color: var(--primary-color);
  font-size: 1.5rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.heart-icon.favorited {
  color: var(--secondary-color);
  text-shadow: var(--primary-color);
}

button {
  background-color: var(--accent-color);
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #2980b9;
}

@media (max-width: 768px) {
  .container {
    width: 95%;
    padding: 1rem;
  }

  .book-list, .favorites-list {
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 1rem;
  }
}
@media (max-width: 480px) {
  .container {
    width: 100%;
    padding: 0.5rem;
  }

  .book-list, .favorites-list {
    grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
    gap: 0.5rem;
  }

  .book-item, .favorite-item {
    font-size: 0.9rem;
  }

  .book-item img, .favorite-item img {
    height: 180px;
  }

  .book-item h3, .favorite-item h3 {
    font-size: 1rem;
  }

  .book-item p, .favorite-item p {
    font-size: 0.8rem;
  }

  h1 {
    font-size: 1.8rem;
  }

  h2 {
    font-size: 1.3rem;
  }

  button {
    padding: 0.4rem 0.8rem;
    font-size: 0.9rem;
  }
}

/* Small Mobile Devices */
@media (max-width: 320px) {
  .book-list, .favorites-list {
    grid-template-columns: 1fr;
  }

  .book-item img, .favorite-item img {
    height: auto;
    max-height: 200px;
  }

  h1 {
    font-size: 1.5rem;
  }

  h2 {
    font-size: 1.2rem;
  }
}
</style>
