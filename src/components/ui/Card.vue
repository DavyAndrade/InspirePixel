<script setup>
import { Heart } from "lucide-vue-next";

defineProps({
  image: {
    type: Object,
    required: true,
  },
});

defineEmits(["toggle-favorite"]);
</script>

<template>
  <div class="image-wrapper">
    <img :src="image.url" :alt="`Photo by ${image.author}`" loading="lazy" />
    <button
      class="favorite-btn"
      @click="$emit('toggle-favorite', image.id)"
      :aria-label="
        image.isFavorite ? 'Remover dos favoritos' : 'Adicionar aos favoritos'
      "
    >
      <Heart
        :class="{ 'is-active': image.isFavorite }"
        :fill="image.isFavorite ? '#ef4444' : 'white'"
        :stroke="image.isFavorite ? '#ef4444' : 'white'"
        :stroke-width="2"
      />
    </button>
  </div>
</template>

<style scoped lang="scss">
.image-wrapper {
  position: relative;
  border-radius: 8px;
  overflow: hidden;
  aspect-ratio: 2/3; // Portrait ratio
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
  width: 100%;

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
