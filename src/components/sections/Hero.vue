<script setup></script>

<template>
  <section class="hero" id="hero">
    <div class="hero__image">
      <img src="../../assets/images/hero.png" alt="Hero" />
    </div>

    <div class="hero__content">
      <h2 class="hero__title">Onde a paisagem vira <span>inspiração</span>.</h2>
      <p class="hero__description">
        Explore paisagens, cores e luzes que inspiram novas histórias através da
        fotografia.
      </p>
    </div>
  </section>
</template>

<style scoped lang="scss">
$text-color: #1f2937;

.hero {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 5rem 1rem;
  gap: 2rem;
  max-width: 1024px;
  min-height: 100vh;
  margin: 0 auto;
  color: $text-color;

  &__image {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    object-fit: cover;
    padding-inline: 2.5rem;
  }

  &__content {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    gap: 2rem;

    .hero__title {
      font-size: 2rem;
      font-weight: 800;
      line-height: 1.5;
      padding-inline: 1rem;

      span {
        font-size: 3rem;
        color: #e1306c;
      }
    }

    .hero__description {
      font-size: 1rem;
      font-weight: 500;
      line-height: 1.2;
    }
  }
}

/* Tablet */
@media screen and (min-width: 768px) {
  .hero {
    display: flex;
    flex-direction: row-reverse;
    justify-content: space-evenly;
    align-items: center;
    gap: 1rem;
    height: 100vh;
    width: 100%;

    &__image {
      width: auto;
      height: auto;
    }

    &__content {
      align-items: start;
      text-align: left;

      .hero__title {
        max-width: 25ch;
        padding-inline: 0;
      }

      .hero__description {
        max-width: 50ch;
        padding-inline: 0;
      }
    }
  }
}
</style>
