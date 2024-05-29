<script>
import Button from './UI/Button.vue';
export default {
  components: {
    Button,
  },
  props: {
    onSentData: {
      type: Function,
      required: true,
    },
  },
  data() {
    return {
      box: {
        img: 'check.svg',
        title: 'Submit your quote request',
        desc: 'Please review all the information you previously typed in the past steps, and if all is okay, submit your message to receive a project quote in 24 - 48 hours.',
      },
    };
  },
};
</script>

<template>
  <div class="form-total-box">
    <img class="form-total-box__img" :src="'/assets/img/' + box.img" alt="" />
    <div class="form-total-box__title">{{ box.title }}</div>
    <div class="form-total-box__desc">{{ box.desc }}</div>
    <Button text="Submit" @click="onSentData"></Button>
  </div>
</template>

<style scoped lang="scss">
.form-total-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  &__img {
    width: 157px;
    height: 143px;
    object-fit: contain;
    margin-bottom: 18px;
  }

  &__title {
    font-weight: 700;
    font-size: 24px;
    line-height: 146%;
    text-align: center;
    color: var(--neutral-800);
    margin-bottom: 7.5px;
  }

  &__desc {
    line-height: 167%;
    text-align: center;
    color: var(--neutral-600);
    margin-bottom: 12px;
  }
}
</style>
