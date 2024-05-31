<script>
export default {
  props: {
    text: {
      type: String,
      required: true,
    },
    light: {
      type: Boolean,
    },
    disabled: {
      type: Boolean,
    },
  },
};
</script>

<template>
  <button class="btn" :class="{ 'btn--light': light }" :disabled="disabled">{{ text }}</button>
</template>

<style scoped lang="scss">
.btn {
  background-color: var(--primary-color-1);
  border-radius: 56px;
  padding: 20px 40px 21px 40px;
  box-shadow: 0 3px 12px 0 rgba(74, 58, 255, 0.18);
  font-weight: 700;
  color: var(--neutral-100);
  user-select: none;

  @media (max-width: 767px) {
    padding: 14px 26px 17px 26px;
    font-size: 15px;
  }

  &--light {
    border: 1px solid var(--primary-color-1);
    color: var(--primary-color-1);
    background: var(--neutral-100);
  }

  &:disabled {
    background-color: rgb(167, 161, 161);
  }
}
</style>
