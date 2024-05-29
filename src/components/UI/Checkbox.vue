<script>
export default {
  props: {
    img: {
      type: String,
    },
    title: {
      type: String,
      required: true,
    },
    checked: {
      type: Boolean,
    },
    ourServices: {
      type: Array,
    },
  },
  methods: {
    onChecked(e) {
      const value = e.target.value;
      if (this.ourServices.includes(value)) {
        let checkboxArray = this.ourServices.filter((item) => item !== value);
        this.$emit('ourServices', checkboxArray);
      } else {
        let checkboxArray = this.ourServices;
        checkboxArray.push(value);
        this.$emit('ourServices', checkboxArray);
      }
    },
  },
  // emits: ['update:ourServices'],
};
</script>

<template>
  <label class="checkbox">
    <input
      class="checkbox__input"
      type="checkbox"
      :value="title"
      @change="onChecked"
      :checked="this.ourServices.includes(this.title)"
    />
    <div class="checkbox__elem">
      <div class="checkbox__elem-icon">
        <img
          class="checkbox__elem-icon-elem"
          :src="'/assets/img/our-services/' + img"
          :alt="title"
        />
      </div>
      <div class="checkbox__elem-title">{{ title }}</div>
    </div>
  </label>
</template>

<style scoped lang="scss">
.checkbox {
  &__input {
    position: absolute;
    width: 1px;
    height: 1px;
    margin: -1px;
    clip: rect(0 0 0 0);

    &:checked + .checkbox__elem {
      border: 2px solid var(--primary-color-1);
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

    @media (max-width: 767px) {
      height: 90px;
    }
  }

  &__elem-icon {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 67px;
    height: 67px;
    border-radius: 100%;
    background-color: rgb(74, 58, 255, 0.15);
    margin-right: 23px;
    padding: 11px;

    @media (max-width: 767px) {
      width: 55px;
      height: 55px;
    }
  }

  &__elem-icon-elem {
    width: 100%;
  }

  &__elem-title {
    font-weight: 500;
    color: var(--neutral-800);
  }
}
</style>
