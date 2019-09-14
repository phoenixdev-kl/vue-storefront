<template>
  <div class="media-gallery">
    <div v-if="isOnline" class="relative w-100">
      <product-gallery-overlay
        v-if="isZoomOpen"
        :current-slide="currentSlide"
        :product-name="product.name"
        :gallery="gallery"
        @close="toggleZoom"
      />
      <no-ssr>
        <product-gallery-carousel
          v-if="showProductGalleryCarousel"
          :gallery="gallery"
          :configuration="configuration"
          :product-name="product.name"
          @toggle="openOverlay"
          @loaded="carouselLoaded = true"
        />
      </no-ssr>
    </div>
    <product-image v-else :image="offline" />
  </div>
</template>

<script>
import { ProductGallery } from '@vue-storefront/core/modules/catalog/components/ProductGallery.ts'
import ProductGalleryOverlay from './ProductGalleryOverlay'
import onEscapePress from '@vue-storefront/core/mixins/onEscapePress'
import NoSSR from 'vue-no-ssr'
import ProductImage from './ProductImage'
import { onlineHelper } from '@vue-storefront/core/helpers'

const ProductGalleryCarousel = () => import(/* webpackChunkName: "vsf-product-gallery-carousel" */ './ProductGalleryCarousel.vue')

export default {
  components: {
    ProductGalleryCarousel,
    'no-ssr': NoSSR,
    ProductGalleryOverlay,
    ProductImage
  },
  mixins: [
    ProductGallery,
    onEscapePress
  ],
  watch: {
    '$route': 'validateRoute'
  },
  data () {
    return {
      isZoomOpen: false,
      showProductGalleryCarousel: false,
      currentSlide: 0,
      carouselLoaded: false
    }
  },
  mounted () {
    this.showProductGalleryCarousel = true
  },
  computed: {
    isOnline (value) {
      return onlineHelper.isOnline
    }
  },
  methods: {
    openOverlay (currentSlide) {
      this.currentSlide = currentSlide
      this.toggleZoom()
    },
    validateRoute () {
      this.$forceUpdate()
    },
    toggleZoom () {
      this.isZoomOpen = !this.isZoomOpen
    },
    onEscapePress () {
      if (this.isZoomOpen) {
        this.toggleZoom()
      }
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~theme/css/variables/media-queries';

.media-gallery {
  text-align: center;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  min-height: calc(90vw * 1.1);

  @include media('o-screen', '>=sm') {
    min-height: inherit;
  }

  &--loaded {
    background-image: none;
  }
}
</style>
