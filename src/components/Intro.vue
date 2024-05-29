<script>
import FormBox1 from './FormBoxs/FormBox1.vue';
import FormBox2 from './FormBoxs/FormBox2.vue';
import FormBox3 from './FormBoxs/FormBox3.vue';

import FormSteps from './FormSteps.vue';
import FormTotalBox from './FormTotalBox.vue';
import Button from './UI/Button.vue';
import RadioButton from './UI/RadioButton.vue';

export default {
  components: {
    FormSteps,
    FormBox1,
    FormBox2,
    FormBox3,
    FormTotalBox,
    Button,
    RadioButton,
  },
  data() {
    return {
      activeStep: 1,
      numberSteps: [1, 2, 3, 4],
      dataToSend: {
        contactDetails: {},
        ourServices: [],
        projectBudget: '',
      },
    };
  },
  methods: {
    onPrevStep() {
      this.activeStep--;
    },
    onNextStep() {
      this.activeStep++;
    },
    onSentData() {
      localStorage.setItem('dataToSend', JSON.stringify(this.dataToSend));
      console.log('GOOD SENT');
    },
  },
};
</script>

<template>
  <div class="intro">
    <div class="container">
      <h1 class="intro__title">Get a project quote</h1>
      <p class="intro__text">
        Please fill the form below to receive a quote for your project. Feel free to add as much
        detail as needed.
      </p>
      <form class="form-main" @submit.prevent="onSentData">
        <FormSteps :activeStep="activeStep" :numberSteps="numberSteps" />
        <FormBox1 v-show="activeStep === 1" v-model:contact-details="dataToSend.contactDetails" />
        <FormBox2 v-show="activeStep === 2" v-model:our-services="dataToSend.ourServices" />
        <FormBox3 v-show="activeStep === 3" v-model:project-budget="dataToSend.projectBudget" />
        <FormTotalBox v-if="activeStep === 4" :onSentData="this.onSentData" />
      </form>
      <div v-if="Object.keys(dataToSend.contactDetails).length === 4" class="buttons">
        <Button
          v-show="activeStep > 1"
          text="Previous step"
          :light="true"
          @click="onPrevStep"
        ></Button>
        <Button v-show="activeStep !== 4" text="Next step" @click="onNextStep"></Button>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.intro {
  max-width: 698px;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin: 56px auto 100px;

  @media (max-width: 767px) {
    margin: 36px auto 70px;
  }

  &__title {
    font-weight: 700;
    font-size: 34px;
    line-height: 135%;
    text-align: center;
    color: var(--neutral-800);
    margin-bottom: 12px;
  }

  &__text {
    max-width: 566px;
    line-height: 167%;
    text-align: center;
    color: var(--neutral-600);
    margin-bottom: 42px;
  }
}

.form-main {
  max-width: 698px;
  width: 100%;
  border: 1px solid var(--neutral-300);
  border-radius: 34px;
  box-shadow: 0 5px 16px 0 rgba(8, 15, 52, 0.06);
  padding: 33px 55px 80px;
  margin: 0 auto;

  @media (max-width: 767px) {
    padding: 30px 20px;
  }
}

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

.buttons {
  display: flex;
  align-items: center;
  justify-content: space-between;
  max-width: 698px;
  width: 100%;
  margin: 31px auto 0;

  .btn {
    &:first-child {
      margin-right: auto;
    }

    &:last-child {
      margin-left: auto;
    }
  }
}
</style>
./UI/InputForm.vue
