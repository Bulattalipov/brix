<script>
import Logo from './Logo.vue';
import InputComponent from './UI/Input.vue';
export default {
  components: {
    Logo,
    InputComponent,
  },
};
</script>

<template>
  <footer class="footer">
    <div class="container">
      <div class="footer__inner">
        <div class="footer__left">
          <Logo isSmall />
          <div class="footer__copyright">Copyright © 2021 BRIX Templates | All Rights Reserved</div>
        </div>
        <div class="footer__subscribe">
          <InputComponent inputType="text" placeholder="Enter your email" withButton />
        </div>
      </div>
    </div>
  </footer>
</template>

<style lang="scss">
.footer {
  border-top: 1px solid var(--neutral-400);
  padding: 57px 0;

  &__inner {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 20px;

    @media (max-width: 1199px) {
      flex-direction: column-reverse;
      gap: 40px;
    }
  }

  &__left {
    @media (max-width: 1199px) {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
  }

  &__copyright {
    line-height: 167%;
    color: var(--neutral-600);
    margin-top: 18px;
  }

  .input {
    width: 507px;

    @media (max-width: 575px) {
      width: 100%;
    }

    &__elem {
      padding-right: 170px;
    }
  }
}
</style>
