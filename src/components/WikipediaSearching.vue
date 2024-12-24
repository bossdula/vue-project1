<script setup>
import { ref } from "vue";

const searchQuery = ref("");
const searchResults = ref([]);
const isLoading = ref(false);
const error = ref(null);
const isDarkTheme = ref(false);

const WIKIPEDIA_API_BASE = "https://en.wikipedia.org/w/api.php";

const searchWikipedia = async (query) => {
  const encodedQuery = encodeURIComponent(query);
  const endpoint = `${WIKIPEDIA_API_BASE}?action=query&list=search&prop=info&inprop=url&utf8=&format=json&origin=*&srlimit=10&srsearch=${encodedQuery}`;

  try {
    isLoading.value = true;
    const response = await fetch(endpoint);
    const data = await response.json();

    if (data.query && data.query.search) {
      searchResults.value = data.query.search;
      error.value = null;
    } else {
      searchResults.value = [];
      error.value = "No results found";
    }
  } catch (error) {
    console.error("Error fetching data:", error);
    searchResults.value = [];
    error.value = "An error occurred while fetching data";
  } finally {
    isLoading.value = false;
  }
};


const toggleTheme = () => {
  isDarkTheme.value = !isDarkTheme.value;
};


const submitSearch = () => {
  if (searchQuery.value.trim() !== "") {
    searchWikipedia(searchQuery.value);
  } else {
    searchResults.value = [];
    error.value = "Please enter a search term.";
  }
};
</script>

<template>
  <div :class="{ 'dark-theme': isDarkTheme }">
    <div class="container">

      <div class="header-container">
        <h1>Search Wikipedia</h1>
        <span id="theme-toggler" @click="toggleTheme">
          {{ isDarkTheme ? "Light" : "Dark" }}
        </span>
      </div>

      <form @submit.prevent="submitSearch">
        <input type="text" v-model="searchQuery" placeholder="Enter search term" />
        <button type="submit">SEARCH</button>
      </form>

      <div id="search-result">

        <div v-if="isLoading" class="spinner">Loading...</div>
        <p v-if="error">{{ error }}</p>
        <div v-if="!isLoading && searchResults.length > 0">
          <div
            v-for="result in searchResults"
            :key="result.pageid"
            class="result-item"
          >
            <h3 class="result-title">
              <a :href="'https://en.wikipedia.org/?curid=' + result.pageid" target="_blank" rel="noopener">{{ result.title }}</a>
            </h3>

            <p>{{ result.snippet }} + <a :href="'https://en.wikipedia.org/?curid=' + result.pageid">More.. &#129074;</a></p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<style scoped>
/* General Theme Styles */
.dark-theme {
  background-color: #121212;
  color: #ffffff;
}

.light-theme {
  background-color: #ffffff;
  color: #121212;
}

.container {
  width: 600px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

/* Header */
.header-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.header-container h1 {
  font-size: 24px;
  margin: 0;
}

#theme-toggler {
  cursor: pointer;
  font-size: 14px;
  padding: 5px 10px;
  border-radius: 4px;
  background-color: #007bff;
  color: white;
  transition: background-color 0.3s;
}

#theme-toggler:hover {
  background-color: #0056b3;
}

/* Form */
form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 20px;
}

form input {
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ddd;
  border-radius: 4px;
  outline: none;
}

form input:focus {
  border-color: #007bff;
  box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

form button {
  padding: 10px;
  font-size: 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

form button:hover {
  background-color: #0056b3;
}

/* Spinner */
.spinner {
  text-align: center;
  font-size: 18px;
  font-weight: bold;
}

/* Results Section */
#search-result {
  margin-top: 20px;
}

.result-item {
  padding: 10px;
  border-bottom: 1px solid #ddd;
}

.result-title a {
  text-decoration: none;
  font-size: 18px;
  color: #007bff;
  transition: color 0.3s;
}

.result-title a:hover {
  color: #0056b3;
}

/* Responsive Design */
@media (max-width: 768px) {
  .container {
    padding: 10px;
  }

  .header-container h1 {
    font-size: 20px;
  }

  form input,
  form button {
    font-size: 14px;
  }
}
</style>

