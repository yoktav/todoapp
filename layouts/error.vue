<template>
  <div class="u-height-100vh">
    <div class="container u-height-100%">
      <div class="c-error-page-wrapper">
        <NuxtLink :to="ROUTE_NAMES.HOME.PATH">
          TODOAPP
          <!-- <img width="200" class="u-object-fit-contain" src="~/assets/img/logo.svg" /> -->
        </NuxtLink>

        <img
          :src="
            require(`~/assets/img/error-${
              error.statusCode === 403
                ? '403'
                : error.statusCode === 404
                ? '404'
                : error.statusCode === 500
                ? '500'
                : ''
            }.png`)
          "
          alt="TODOAPP-HATA"
          class="c-error-image"
        />

        <div class="u-text-align-center">
          <p class="u-font-size-4xlarge u-margin-bottom-2xlarge">
            <strong>Oops</strong>,
            {{
              error.statusCode === 403
                ? 'Bu Sayfaya Erişim Yetkiniz Yok!'
                : error.statusCode === 404
                ? 'Aradığınız Sayfa Bulunamadı.'
                : error.statusCode === 500
                ? 'Sistemsel Bir Sorun Yaşandı.'
                : 'Bir hata oluştu'
            }}
          </p>

          <Button theme="primary" class="c-home-button" tag="NuxtLink" :to="ROUTE_NAMES.HOME.PATH"
            >Ana sayfaya dön
          </Button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ROUTE_NAMES } from '~/project-constants/routeNames';

export default {
  layout: 'error',

  props: {
    error: {
      type: Object,
      default: null,
    },
  },

  data() {
    return {
      ROUTE_NAMES,
    };
  },

  mounted() {
    this.$nextTick(() => {
      this.$nuxt.$loading.finish();
    });
  },
};
</script>

<style lang="scss" scoped>
@import '../assets/styles/abstracts/index';

.c-error-page-wrapper {
  display: grid;
  height: 100%;
  place-items: center;
}

.c-error-image {
  max-width: 100%;
  animation: bounce 1s infinite alternate;
}

// stylelint-disable declaration-no-important
// Use important to override .c-button styles
.c-home-button {
  font-size: $g-font-size-xlarge !important;
  font-weight: 600 !important;

  @include media-breakpoint-up(xl) {
    padding: pad(small) pad(3xlarge) !important;
  }
}
// stylelint-enable declaration-no-important
</style>
