<template>
  <div class="c-content-block">
    <slot />
  </div>
</template>

<script>
export default {
  name: 'ContentBlock'
}
</script>

<style lang="scss">
  .c-content-block {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  @media screen and (min-width: 768px) {
    .c-content-block {
      flex-direction: row;
      justify-content: space-evenly;
    }
  }
</style>