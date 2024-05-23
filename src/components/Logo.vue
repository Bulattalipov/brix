<script>
export default {
  props: {
    isSmall: {
      type: Boolean,
    },
  },
};
</script>

<template>
  <a class="logo" href="/">
    <img
      class="logo__img"
      :class="{ 'logo__img--small': isSmall }"
      src="/assets/img/logo.svg"
      alt="logo"
    />
  </a>
</template>

<style scoped lang="scss">
.logo {
  &__img {
    &--small {
      width: 264px;
      height: 36px;
    }

    @media (max-width: 767px) {
      width: 235px;
    }
  }
}
</style>
