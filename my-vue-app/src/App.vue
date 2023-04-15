<template>
  <div id="app">
    <div class="top-bar">
      <button
        v-for="category in categories"
        :key="category"
        :class="[
          'category-button',
          'animate__animated',
          hoverCategory === category ? 'animate__pulse' : '',
          selectedCategory === category ? 'selected' : '',
        ]"
        @mouseover="hoverCategory = category"
        @mouseout="hoverCategory = null"
        @click="selectCategory(category)"
      >
        {{ category }}
      </button>
    </div>
    <div class="main-content">
      <input type="file" @change="uploadImage" />
      <div v-if="uploadedImage" class="uploaded-image">
        <img :src="uploadedImage" alt="Uploaded" />
        <div class="convert-container">
          <button
            v-if="selectedCategory"
            class="convert-button animate__animated animate__pulse"
            :class="`convert-button--${selectedCategory.toLowerCase()}`"
            @click="convertImage"
          >
            <span>Convert</span>
            <i class="fas fa-sync-alt"></i>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import "animate.css";

export default {
  data() {
    return {
      hoverCategory: null,
      selectedCategory: "Category 1",
      categories: ["Category 1", "Category 2", "Category 3"],
      uploadedImage: null,
    };
  },
  methods: {
    selectCategory(category) {
      this.selectedCategory = category;
    },
    uploadImage(event) {
      const file = event.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = (e) => {
          this.uploadedImage = e.target.result;
        };
        reader.readAsDataURL(file);
      }
    },
    convertImage() {
      if (!this.selectedCategory) return;
      // Implement the conversion logic based on the selected category
      alert(`Converting image using ${this.selectedCategory}`);
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap");

#app {
  font-family: "Poppins", sans-serif;
  text-align: center;
  background-color: #f5f5f5;
  min-height: 100vh;
}

.top-bar {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
  padding: 20px;
  background-color: #222;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
}

.category-button {
  font-size: 18px;
  margin: 0 10px;
  padding: 10px 20px;
  border: none;
  background-color: transparent;
  color: #fff;
  cursor: pointer;
  outline: none;
  transition: color 0.3s, font-weight 0.3s;
}

.category-button:hover {
  color: #64b5f6;
}

.category-button.selected {
  font-weight: 600;
  color: #64b5f6;
}

.main-content {
  padding: 20px;
}

input[type="file"] {
  font-size: 16px;
  margin-bottom: 20px;
  cursor: pointer;
}

.uploaded-image {
  position: relative;
}

.uploaded-image img {
  max-width: 100%;
  height: auto;
  margin-top: 20px;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
}

.convert-container {
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
}

.convert-button {
  display: inline-block;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  font-size: 18px;
  font-weight: 600;
  color: #fff;
  background-color: #4caf50;
  cursor: pointer;
  outline: none;
  transition: background-color 0.3s, transform 0.3s;
}

.convert-button span {
  display: inline-block;
  margin-right: 10px;
}

.convert-button--category-1 {
  background-color: #64b5f6;
}

.convert-button--category-2 {
  background-color: #f06292;
}

.convert-button--category-3 {
  background-color: #4caf50;
}

.convert-button:hover {
  opacity: 0.8;
  transform: scale(1.1);
}

.convert-button i {
  margin-left: 10px;
  animation: rotate 1s linear infinite;
}

@keyframes rotate {
  100% {
    transform: rotate(360deg);
  }
}
</style>
