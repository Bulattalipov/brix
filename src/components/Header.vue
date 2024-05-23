<script>
import Logo from './Logo.vue';
import Button from './UI/Button.vue';
export default {
  components: {
    Button,
    Logo,
  },
};
</script>

<template>
  <header class="header">
    <div class="container">
      <div class="header__inner">
        <Logo />
        <Button text="Clone now"></Button>
      </div>
    </div>
  </header>
</template>

<style scoped lang="scss">
.header {
  &__inner {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 32px 0;
  }
}
</style>
