<script setup>
import { ref, onMounted } from "vue";
import { Heart } from "lucide-vue-next";

const images = ref([]);

const fetchImages = async () => {
  try {
    // Randomize page to get different images (avoiding the default "computer" heavy page 1)
    const randomPage = Math.floor(Math.random() * 20) + 1;
    const response = await fetch(
      `https://picsum.photos/v2/list?page=${randomPage}&limit=12`
    );
    const data = await response.json();
    images.value = data.map((img) => ({
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
        <div class="image-wrapper">
          <img
            :src="image.url"
            :alt="`Photo by ${image.author}`"
            loading="lazy"
          />
          <button
            class="favorite-btn"
            @click="toggleFavorite(image.id)"
            :aria-label="
              image.isFavorite
                ? 'Remover dos favoritos'
                : 'Adicionar aos favoritos'
            "
          >
            <Heart
              :class="{ 'is-active': image.isFavorite }"
              :fill="image.isFavorite ? '#ef4444' : 'none'"
              :stroke="image.isFavorite ? '#ef4444' : 'white'"
              :stroke-width="2"
            />
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped lang="scss">
.gallery-section {
  padding: 2rem 1rem;
  max-width: 1024px;
  margin: 0 auto;
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

.image-wrapper {
  position: relative;
  border-radius: 8px;
  overflow: hidden;
  aspect-ratio: 2/3; // Portrait ratio
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;

  &:hover {
    transform: translateY(-4px);
  }

  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    display: block;
  }
}

.favorite-btn {
  position: absolute;
  top: 10px;
  right: 10px;
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 5px;
  transition: transform 0.2s ease;
  z-index: 10;

  &:hover {
    transform: scale(1.1);
  }

  svg {
    width: 24px;
    height: 24px;
    filter: drop-shadow(
      0 2px 4px rgba(0, 0, 0, 0.3)
    ); // Shadow for visibility on light images
    transition: all 0.3s ease;
  }
}
</style>
