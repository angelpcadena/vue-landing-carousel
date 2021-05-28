<template>
  <a class="c-button" :href="Href" target="_blank">
    <slot />
  </a>
</template>

<script>
export default {
  name: "Button",
  props: ["Href", "CustomClass"]
}
</script>

<style lang="scss">
  .c-button {
    background-color: #81c784;
    color: white;
    display: inline-block;
    font-size: 1rem;  
    text-decoration: none;
    line-height: 1;
    padding: .5rem 1rem;
    border-radius: .25rem;
    transition: box-shadow ease-in-out 100ms;

    &:hover {
      box-shadow: inset 0 0 2rem 2rem rgba(0, 0, 0, .15);
    }
  }
</style>