<script>
export default {
  props: {
    activeStep: {
      type: Number,
      required: true,
    },
    numberSteps: {
      type: Array,
      required: true,
    },
  },
};
</script>

<template>
  <div class="form-steps">
    <div
      v-for="numberStep in numberSteps"
      :key="numberStep"
      :class="{ 'form-steps__item--active': numberStep <= activeStep }"
      class="form-steps__item"
    >
      <div class="form-steps__item-number">
        <span>{{ numberStep }}</span>
      </div>
      <div class="form-steps__item-line"></div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.form-steps {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 18px;
  padding-bottom: 32px;
  margin-bottom: 64px;
  border-bottom: 1px solid var(--neutral-400);

  @media (max-width: 767px) {
    margin-bottom: 40px;
    gap: 10px;
  }

  @media (max-width: 575px) {
    gap: 20px;
    margin-bottom: 30px;
    padding-bottom: 20px;
  }

  &__item {
    display: flex;
    align-items: center;
    gap: 18px;

    &:first-child {
      &::before {
        display: none;
      }
    }

    &:last-child {
      .form-steps__item-line {
        display: none;
      }
    }

    @media (max-width: 767px) {
      gap: 10px;
    }

    &--active {
      position: relative;

      &::before {
        content: '';
        position: absolute;
        top: 14px;
        left: -116px;
        width: 98px;
        height: 6px;
        background-color: #4a3aff;
        border-radius: 40px;

        @media (max-width: 767px) {
          left: -54px;
          width: 45px;
        }

        @media (max-width: 575px) {
          display: none;
        }
      }

      .form-steps__item-number {
        color: #fff;
        background-color: #4a3aff;
      }

      .form-steps__item-line {
        position: relative;

        &::after {
          content: '';
          position: absolute;
          top: 0;
          left: 0;
          height: 100%;
          width: 50%;
          background-color: #4a3aff;
          border-radius: 40px;

          @media (max-width: 575px) {
            display: none;
          }
        }
      }
    }
  }

  &__item-number {
    width: 34px;
    height: 34px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    fill: var(--neutral-300);
    font-weight: 400;
    font-size: 16px;
    line-height: 144%;
    color: var(--neutral-600);
    background-color: #eff0f7;
  }

  &__item-line {
    border-radius: 40px;
    width: 98px;
    height: 6px;
    background: var(--neutral-300);

    @media (max-width: 767px) {
      width: 45px;
    }

    @media (max-width: 575px) {
      display: none;
    }
  }
}
</style>
