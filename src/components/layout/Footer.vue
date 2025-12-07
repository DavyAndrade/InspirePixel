<script setup>
import { Facebook, Linkedin, Instagram, Twitter } from "lucide-vue-next";
</script>

<template>
  <footer class="footer">
    <div class="footer__container">
      <!-- Newsletter Section -->
      <div class="footer__section footer__section--newsletter">
        <h3 class="footer__title">Assine nossa newsletter</h3>
        <form class="footer__form" @submit.prevent>
          <input type="email" placeholder="Seu email" class="footer__input" />
          <button type="submit" class="footer__button">Inscrever-se</button>
        </form>
      </div>

      <!-- Contact Section -->
      <div class="footer__section footer__section--contact">
        <h3 class="footer__title">Contato</h3>
        <div class="footer__info">
          <p>contato@inspiralens.com</p>
          <p>Central de ajuda</p>
          <p>Rio de Janeiro - Brasil</p>
        </div>
      </div>

      <!-- About Section -->
      <div class="footer__section footer__section--about">
        <h3 class="footer__title">Sobre</h3>
        <ul class="footer__links">
          <li><a href="#">Politicas</a></li>
          <li><a href="#">Politicas de privacidade</a></li>
          <li><a href="#">Blog</a></li>
        </ul>
      </div>

      <!-- Social Icons -->
      <div class="footer__socials">
        <a href="#" aria-label="Facebook"><Facebook /></a>
        <a href="#" aria-label="LinkedIn"><Linkedin /></a>
        <a href="#" aria-label="Instagram"><Instagram /></a>
        <a href="#" aria-label="Twitter"><Twitter /></a>
      </div>
    </div>
  </footer>
</template>

<style scoped lang="scss">
$primary-color: #e1306c;
$text-color: #333;
$light-gray: #f9fafb;

.footer {
  background-color: #fff;
  padding: 4rem 1rem 3rem;
  color: $text-color;
  border-top: 1px solid #eee;
  margin-top: 4rem;

  &__container {
    max-width: 1200px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr;
    gap: 3rem;
    text-align: center;
  }

  &__section {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  &__title {
    font-size: 1.25rem;
    font-weight: 700;
    color: #111;
    margin-bottom: 0.5rem;
  }

  &__info p,
  &__links li {
    margin-bottom: 0.5rem;
    font-size: 0.95rem;
    color: #555;
  }

  &__links a {
    text-decoration: none;
    transition: color 0.2s;

    &:hover {
      color: $primary-color;
    }
  }

  &__form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    align-items: center;
    width: 100%;
    max-width: 400px;
    margin: 0 auto;
  }

  &__input {
    width: 100%;
    padding: 0.75rem 1rem;
    border: none;
    background-color: $light-gray;
    border-radius: 4px;
    font-size: 0.9rem;
    outline: none;

    &:focus {
      box-shadow: 0 0 0 2px rgba($primary-color, 0.2);
    }
  }

  &__button {
    background-color: $primary-color;
    color: white;
    padding: 0.75rem 2rem;
    border: none;
    border-radius: 4px;
    font-weight: 600;
    cursor: pointer;
    transition: background-color 0.2s;
    width: 100%;

    &:hover {
      background-color: darken($primary-color, 5%);
    }
  }

  &__socials {
    display: flex;
    justify-content: center;
    gap: 1.5rem;
    margin-top: 1rem;

    a {
      color: #333;
      transition: color 0.2s, transform 0.2s;

      &:hover {
        color: $primary-color;
        transform: translateY(-2px);
      }
    }
  }

  // Desktop Styles
  @media (min-width: 768px) {
    &__container {
      grid-template-columns: 1fr 1fr 1.5fr;
      grid-template-areas:
        "contact about newsletter"
        "socials socials socials";
      text-align: left;
      align-items: start;
      padding-inline: 2rem;
    }

    &__section--newsletter {
      grid-area: newsletter;
      align-items: flex-start; // Align form to left
    }

    &__section--contact {
      grid-area: contact;
    }

    &__section--about {
      grid-area: about;
    }

    &__socials {
      grid-area: socials;
      margin-top: 4rem;
      justify-content: center; // Keep socials centered
    }

    &__form {
      align-items: flex-start; // Align input/button to left
      margin: 0; // Remove auto margin
    }

    &__button {
      width: auto; // Button auto width on desktop
    }
  }
}
</style>
