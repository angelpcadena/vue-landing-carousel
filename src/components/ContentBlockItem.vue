<template>
  <div class="c-content-block__item">
    <div class="c-content-block__item__title">
      <div class="c-content-block__item__title__icon">
        <svg :class="`icon icon-${Icon}`">
          <use :xlink:href="require('@/assets/icons/symbol-defs.svg') + `#icon-${Icon}`"></use>
        </svg>
      </div>
      <div class="c-content-block__item__title__text">
        {{ Title }}
      </div>
    </div>
    <div class="c-content-block__item__content">
      <slot />
    </div>
    <Button :href="CtaLink">{{CtaText}}</Button>
  </div>
</template>

<script>
export default {
  name: 'ContentBlockItem',
  props: ["Icon", "Title", "CtaText", "CtaLink"]
}
</script>

<style lang="scss">
  .c-content-block__item {
    flex: 1 0;
    margin: 0 2rem;
    margin-bottom: 2rem;

    &__title {
      display: flex;
      align-items: center;
      margin-bottom: 1rem;
      flex-wrap: wrap;

      &__icon {
        font-size: 1.5rem;
        display: inline;
        margin-right: .5rem;
      }

      &__text {
        font-weight: 600;
      }
    }

    &__content {
      min-height: calc(1rem * 3);
      margin-bottom: 1rem;
    }
  }

  @media screen and (min-width: 768px) {
    .c-content-block__item {
      margin-bottom: 0;
    }
  }
</style>