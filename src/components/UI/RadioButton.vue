<script>
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
    projectBudget: {
      type: String,
    },
  },
};
</script>

<template>
  <label class="radio-button">
    <input
      class="radio-button__input"
      type="radio"
      name="budget"
      :value="title"
      :checked="projectBudget === title"
      @change="$emit('update:projectBudget', $event.target.value)"
    />
    <div class="radio-button__elem">
      <div class="radio-button__elem-circle"></div>
      <div class="radio-button__elem-title">{{ title }}</div>
    </div>
  </label>
</template>

<style scoped lang="scss">
.radio-button {
  &__input {
    position: absolute;
    width: 1px;
    height: 1px;
    margin: -1px;
    clip: rect(0 0 0 0);

    &:checked + .radio-button__elem {
      border: 2px solid var(--primary-color-1);

      .radio-button__elem-circle {
        &::before {
          content: '';
          width: 9.7px;
          height: 9.7px;
          border: 8.65px solid #4a3aff;
          border-radius: 50%;
          flex-shrink: 0;
        }
      }
    }
  }
  &__elem {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 114px;
    border-radius: 16px;
    border: 2px solid transparent;
    box-shadow: 0 4px 10px 0 rgba(31, 37, 89, 0.07), 0 2px 11px 0 rgba(69, 65, 164, 0.06);
    transition: border 0.4s;
    user-select: none;
    cursor: pointer;
  }

  &__elem-circle {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 25px;
    height: 25px;
    border-radius: 50%;
    box-shadow: inset 0 -3px 7px 0 rgba(20, 20, 43, 0.08);
    border: 1.2px solid var(--neutral-400);
    margin-right: 13px;
  }

  &__elem-title {
    font-weight: 500;
    color: var(--neutral-800);
  }
}
</style>
