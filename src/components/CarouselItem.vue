<template>
  <div class="c-carousel__slide">
    <div class="c-carousel__slide__content">
      <h2 class="c-carousel__slide__title">
        {{ HeaderText }}
      </h2>
      <div class="c-carousel__slide__main-text">
        <slot />
      </div>
      <Button :href="CtaLink">{{CtaText}}</Button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CarouselItem',
  props: ['HeaderText' ,'CtaText', 'CtaLink']
}
</script>

<style lang="scss">
  .c-carousel__slide {
    flex: 1 0 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 65vh;
    min-height: 400px;

    &__content {
      text-align: center;
      width: 60%;
      max-width: 800px;
    }

    &__title,
    &__main-text {
      color: white;
      font-size: 1.25rem;
    }

    &__title {
      margin-top: 0;
      padding: 0;
      line-height: 1;
      margin-bottom: 1rem;
    }

    &__main-text {
      min-height: calc(1em * 3);
      margin-bottom: 1rem;
    }

    .c-button {
      padding-left: 3rem;
      padding-right: 3rem;
    }
  }
</style>