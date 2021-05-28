<template>
  <div id="app" class="c-main-app">
    <div class="c-main-app__carousel">
      <Carousel :options=carouselOptions>
        <CarouselItem header-text="Title 1" cta-text="Learn more" cta-link="https://google.com">
          <p>Slide content 1</p>
        </CarouselItem>
        <CarouselItem header-text="Title 2" cta-text="View more" cta-link="https://google.com">
          <p>Slide content 2</p>
        </CarouselItem>
        <CarouselItem header-text="Title 3" cta-text="Know more" cta-link="https://google.com">
          <p>Slide content 3, longer text for testing purposes, this thing on? test test test</p>
        </CarouselItem>
      </Carousel>
    </div>
    <div class="c-main-app__content-block">
      <ContentBlock>
        <ContentBlockItem title="Title for content 1" icon="compass" cta-text="Take me there" cta-link="https://google.com">
          <p>
            Content Block Item 1
          </p>
        </ContentBlockItem>
        <ContentBlockItem title="Title for content 2" icon="coffee" cta-text="Find out" cta-link="https://google.com">
          <p>
            Content Block Item 2
          </p>
        </ContentBlockItem>
        <ContentBlockItem title="Title for content 3" icon="gift" cta-text="You bet" cta-link="https://google.com">
          <p>
            Content Block Item 3 with more text, testing the wrapping
          </p>
        </ContentBlockItem>
      </ContentBlock>
    </div>
  </div>
</template>

<script>
import Carousel from './components/Carousel.vue'
import CarouselItem from './components/CarouselItem.vue'
import ContentBlock from './components/ContentBlock.vue'
import ContentBlockItem from './components/ContentBlockItem.vue'

let carouselOptions = { // all defaults are true if bool
  //autoplay: false,
  //showNavigation: false,
  //showPagination: false
}

export default {
  name: 'App',
  components: {
    Carousel,
    CarouselItem,
    ContentBlock,
    ContentBlockItem
  },
  data() {
    return {
      carouselOptions: carouselOptions
    }
  }
}
</script>

<style lang="scss">
html, body {
  margin: 0;
  padding: 0;
}

p {
  margin: 0;
}
.c-main-app {
  font-family: Roboto, Arial, sans-serif;
  font-size: 16px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  &__carousel {
    margin-bottom: 2rem;
  }
}

.icon {
  display: inline-block;
  width: 1em;
  height: 1em;
  stroke-width: 0;
  stroke: currentColor;
  fill: currentColor;
}

</style>
