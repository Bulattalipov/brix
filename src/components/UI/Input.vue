<script>
import Button from './Button.vue';
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
    inputType: {
      type: String,
      required: true,
    },
    placeholder: {
      type: String,
      required: true,
    },
    imgName: {
      type: String,
    },
    contactDetails: {
      type: Object,
    },
    withButton: {
      type: Boolean,
    },
  },
  components: {
    Button,
  },
  data() {
    return {};
  },
  methods: {
    onChangeInputs(e) {
      let currentContactDetals = this.contactDetails;
      currentContactDetals[this.title] = e.target.value;
      this.$emit('update:contactDetails', currentContactDetals);
    },
  },
  emits: ['update:contactDetails'],
};
</script>

<template>
  <div class="input">
    <div v-if="title" class="input__title">{{ title }}</div>
    <div class="input__inner">
      <input
        class="input__elem"
        :type="inputType"
        :placeholder="placeholder"
        @input="onChangeInputs"
      />
      <img
        v-if="imgName"
        class="input__icon"
        :src="'assets/img/input-icons/' + imgName"
        alt="Name"
      />
      <Button v-if="withButton" text="Subscribe"></Button>
    </div>
  </div>
</template>

<style scoped lang="scss">
.input {
  &__title {
    font-weight: 500;
    line-height: 111%;
    color: var(--neutral-800);
    margin-bottom: 18px;
  }

  &__inner {
    position: relative;
    display: flex;
    align-items: center;
  }

  &__elem {
    width: 100%;
    border: 1px solid var(--neutral-300);
    border-radius: 46px;
    box-shadow: 0 2px 6px 0 rgba(19, 18, 66, 0.07);
    padding: 21px 55px 24px 20px;
    border: 2px solid transparent;
    font-size: 18px;

    &:hover {
      box-shadow: 0 2px 6px 0 rgba(94, 92, 247, 0.07);
    }

    &:focus,
    &:active {
      outline: none;
      border: 2px solid #4a3aff;
    }
  }

  &__icon {
    position: absolute;
    top: 50%;
    right: 20px;
    transform: translateY(-50%);
    width: 23px;
    height: 28px;
    object-fit: contain;
  }

  .btn {
    position: absolute;
    right: 17px;
    padding: 14px 26px 17px 26px;
  }
}
</style>
