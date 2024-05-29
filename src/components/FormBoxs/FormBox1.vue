<script>
import InputComponent from '../UI/Input.vue';
export default {
  components: {
    InputComponent,
  },
  props: {
    contactDetails: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      box: {
        title: 'Contact details',
        text: 'Lorem ipsum dolor sit amet consectetur adipisc.',
        inputs: [
          {
            id: 1,
            title: 'Name',
            inputType: 'text',
            placeholder: 'John Carter',
            imgName: 'name.svg',
          },
          {
            id: 2,
            title: 'Email',
            inputType: 'text',
            placeholder: 'Email address',
            imgName: 'email.svg',
          },
          {
            id: 3,
            title: 'Phone Number',
            inputType: 'tel',
            placeholder: '(123) 456 - 7890',
            imgName: 'phone.svg',
          },
          {
            id: 4,
            title: 'Company',
            inputType: 'text',
            placeholder: 'Company name',
            imgName: 'company.svg',
          },
        ],
      },
      currentContactDetals: this.contactDetails,
    };
  },
};
</script>

<template>
  <div class="form-box">
    <div class="form-box__title">{{ box.title }}</div>
    <div class="form-box__desc">{{ box.text }}</div>
    <div class="form-box__items">
      <div v-for="item in box.inputs" :key="item.id" class="form-box__item">
        <InputComponent v-bind="item" v-model:contact-details="currentContactDetals" />
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.form-box {
  &__title {
    font-weight: 700;
    font-size: 24px;
    line-height: 146%;
    color: var(--neutral-800);
    margin-bottom: 7.5px;
  }

  &__desc {
    color: var(--neutral-600);
  }

  &__items {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 28px;
    margin-top: 40px;

    @media (max-width: 767px) {
      grid-template-columns: repeat(1, 1fr);
      margin-top: 35px;
    }

    @media (max-width: 575px) {
      gap: 22px;
    }
  }
}
</style>
