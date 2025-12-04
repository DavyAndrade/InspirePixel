<script setup>
import { ref } from "vue";
import { X } from "lucide-vue-next";

const menuOpen = ref(false);

const toggleMenu = () => {
  menuOpen.value = !menuOpen.value;
  if (menuOpen.value) {
    document.body.style.overflow = "hidden";
  } else {
    document.body.style.overflow = "";
  }
};
</script>

<template>
  <header class="navbar">
    <!-- Mobile Container (< 768px) -->
    <div class="navbar__mobile">
      <a href="#" class="navbar__logo">
        <img src="../../assets/icons/logo.svg" alt="Logo InspirePixel" />
      </a>

      <div class="navbar__mobile-actions">
        <!-- Search Mobile -->
        <button class="navbar__search-btn" aria-label="Search">
          <img src="../../assets/icons/button-search.svg" alt="Search" />
        </button>

        <button
          @click="toggleMenu"
          class="navbar__menu-toggle"
          aria-label="Toggle menu"
        >
          <transition name="fade" mode="out-in">
            <img
              v-if="!menuOpen"
              src="../../assets/icons/icon-menu-mobile.svg"
              alt="Menu"
            />
            <X v-else class="icon-close" />
          </transition>
        </button>
      </div>
    </div>

    <!-- Tablet/Desktop Container (>= 768px) -->
    <div class="navbar__desktop">
      <a href="#" class="navbar__logo">
        <img src="../../assets/icons/logo.svg" alt="Logo InspirePixel" />
      </a>

      <div class="navbar__desktop-content">
        <!-- Search -->
        <button class="navbar__search-btn" aria-label="Search">
          <img src="../../assets/icons/button-search.svg" alt="Search" />
        </button>

        <!-- Navigation Items -->
        <nav class="navbar__nav">
          <ul class="navbar__links">
            <li><a href="#" class="navbar__link">Início</a></li>
            <li><a href="#" class="navbar__link">Galeria</a></li>
            <li><a href="#" class="navbar__link">Favoritos</a></li>
          </ul>
        </nav>

        <!-- User Button -->
        <button class="navbar__user-btn">
          <img src="../../assets/icons/button-user.svg" alt="User" />
        </button>
      </div>
    </div>

    <!-- Mobile Menu Overlay -->
    <transition name="slide-fade">
      <div class="navbar__mobile-menu" v-if="menuOpen">
        <nav>
          <ul class="navbar__mobile-links">
            <li>
              <a href="#" class="navbar__mobile-link" @click="toggleMenu"
                >Início</a
              >
            </li>
            <li>
              <a href="#" class="navbar__mobile-link" @click="toggleMenu"
                >Galeria</a
              >
            </li>
            <li>
              <a href="#" class="navbar__mobile-link" @click="toggleMenu"
                >Favoritos</a
              >
            </li>
            <li>
              <a href="#" class="navbar__mobile-link" @click="toggleMenu"
                >Entrar</a
              >
            </li>
          </ul>
        </nav>
      </div>
    </transition>
  </header>
</template>

<style scoped lang="scss">
/* Variables */
$primary-color: #e1306c;
$text-color: #1f2937;
$bg-color: rgba(255, 255, 255, 0.85);
$border-color: #e5e7eb;
$transition-speed: 0.3s;

.navbar {
  position: sticky;
  top: 0;
  left: 0;
  z-index: 1000;
  width: 100%;
  background-color: $bg-color;
  backdrop-filter: blur(12px);

  /* Common Logo Styles */
  &__logo {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    text-decoration: none;

    img {
      width: 2.5rem;
      height: 2.5rem;
      transition: transform $transition-speed ease;
    }

    &:hover img {
      transform: scale(1.1);
    }
  }

  /* Mobile Container */
  &__mobile {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 1.5rem;
    height: 5rem;
    max-width: 1280px;
    margin: 0 auto;

    @media (min-width: 768px) {
      display: none;
    }
  }

  &__mobile-actions {
    display: flex;
    align-items: center;
    gap: 1rem;
  }

  &__menu-toggle {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 2.5rem;
    height: 2.5rem;
    color: $text-color;
    z-index: 1001;

    .icon-close {
      width: 1.5rem;
      height: 1.5rem;
      color: $primary-color;
    }
  }

  /* Desktop Container */
  &__desktop {
    display: none;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 1.5rem;
    height: 5rem;
    max-width: 1280px;
    margin: 0 auto;
    height: 100%;

    @media (min-width: 768px) {
      display: flex;
    }
  }

  &__desktop-content {
    display: flex;
    align-items: center;
    gap: 2rem;
  }

  &__search-btn {
    width: 2rem;
    height: 2rem;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    transition: background-color $transition-speed ease;

    &:hover {
      background-color: rgba(0, 0, 0, 0.05);
    }

    img {
      width: 1.5rem;
      height: 1.5rem;
    }
  }

  &__links {
    display: flex;
    gap: 2rem;
    list-style: none;
  }

  &__link {
    font-weight: 400;
    color: $text-color;
    font-size: 1rem;
    position: relative;
    padding: 0.5rem 0;
    transition: color $transition-speed ease;

    &::after {
      content: "";
      position: absolute;
      bottom: 0;
      left: 0;
      width: 0;
      height: 2px;
      background-color: $primary-color;
      transition: width $transition-speed ease;
    }

    &:hover {
      color: $primary-color;

      &::after {
        width: 100%;
      }
    }
  }

  &__user-btn {
    width: 2.5rem;
    height: 2.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    transition: background-color $transition-speed ease;

    &:hover {
      background-color: rgba(0, 0, 0, 0.05);
    }

    img {
      width: 1.5rem;
      height: 1.5rem;
    }
  }

  /* Mobile Menu Overlay */
  &__mobile-menu {
    position: fixed;
    top: 5rem;
    left: 0;
    width: 100%;
    height: calc(100vh - 5rem);
    background-color: #fff;
    padding: 2rem;
    display: flex;
    flex-direction: column;

    @media (min-width: 768px) {
      display: none;
    }
  }

  &__mobile-links {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
    list-style: none;
    text-align: center;
  }

  &__mobile-link {
    font-size: 1.5rem;
    font-weight: 600;
    color: $text-color;
    display: block;
    padding: 0.5rem;
    transition: color $transition-speed;

    &:hover {
      color: $primary-color;
    }
  }
}

/* Animations */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.slide-fade-enter-active {
  transition: all 0.3s ease-out;
}

.slide-fade-leave-active {
  transition: all 0.3s cubic-bezier(1, 0.5, 0.8, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateY(-20px);
  opacity: 0;
}
</style>
