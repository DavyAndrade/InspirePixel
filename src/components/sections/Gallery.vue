<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import Card from "../ui/Card.vue";

const images = ref([]);

const fetchImages = async () => {
  try {
    // Randomize page to get different images (avoiding the default "computer" heavy page 1)
    const randomPage = Math.floor(Math.random() * 20) + 1;
    const response = await axios.get(
      `https://picsum.photos/v2/list?page=${randomPage}&limit=12`
    );
    images.value = response.data.map((img) => ({
      id: img.id,
      url: `https://picsum.photos/id/${img.id}/600/900`, // Portrait aspect ratio
      author: img.author,
      isFavorite: false,
    }));
  } catch (error) {
    console.error("Error fetching images:", error);
  }
};

const toggleFavorite = (id) => {
  const image = images.value.find((img) => img.id === id);
  if (image) {
    image.isFavorite = !image.isFavorite;
  }
};

onMounted(() => {
  fetchImages();
});
</script>

<template>
  <section class="gallery-section" id="gallery">
    <h2 class="gallery-title">Inspire-se</h2>

    <div class="gallery-grid">
      <div v-for="image in images" :key="image.id" class="gallery-item">
        <Card :image="image" @toggle-favorite="toggleFavorite" />
      </div>
    </div>
  </section>
</template>

<style scoped lang="scss">
.gallery-section {
  padding: 2rem 1rem;
  max-width: 768px;
  margin: 0 auto;

  @media (min-width: 1024px) {
    max-width: 1024px;
  }
}

.gallery-title {
  font-size: 1.5rem;
  font-weight: 600;
  color: #333;
  margin-bottom: 1.5rem;
}

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr); // Mobile: 2 columns
  gap: 1rem;

  @media (min-width: 768px) {
    grid-template-columns: repeat(3, 1fr); // Tablet: 3 columns
  }

  @media (min-width: 1024px) {
    grid-template-columns: repeat(4, 1fr); // Desktop: 4 columns
  }
}

.gallery-item {
  // Mobile: Show up to 6 images (hide 7+)
  &:nth-child(n + 7) {
    display: none;
  }

  // Tablet: Show up to 9 images (hide 10+)
  @media (min-width: 768px) {
    &:nth-child(n + 7) {
      display: block;
    }
    &:nth-child(n + 10) {
      display: none;
    }
  }

  // Desktop: Show up to 12 images (show all)
  @media (min-width: 1024px) {
    &:nth-child(n + 10) {
      display: block;
    }
  }
}
</style>
