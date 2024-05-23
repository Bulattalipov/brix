<script>
import FormSteps from './FormSteps.vue';
import FormTotalBox from './FormTotalBox.vue';
import Button from './UI/Button.vue';
import InputComponent from './UI/Input.vue';
import Checkbox from './UI/Checkbox.vue';
import RadioButton from './UI/RadioButton.vue';
export default {
  components: {
    FormSteps,
    FormTotalBox,
    Button,
    InputComponent,
    Checkbox,
    RadioButton,
  },
  data() {
    return {
      activeStep: 1,
      numberSteps: [1, 2, 3, 4],
      boxs: {
        box1: {
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
        box2: {
          title: 'Our services',
          text: 'Please select which service you are interested in.',
          checkboxs: [
            {
              id: 1,
              img: 'development.svg',
              title: 'Development',
              checked: true,
            },
            {
              id: 2,
              img: 'wed-design.svg',
              title: 'Web Design',
              checked: false,
            },
            {
              id: 3,
              img: 'marketing.svg',
              title: 'Marketing',
              checked: false,
            },
            {
              id: 4,
              img: 'Setting.svg',
              title: 'Other',
              checked: false,
            },
          ],
        },
        box3: {
          title: 'What’s your project budget?',
          text: 'Please select the project budget range you have in mind.',
          radioButtons: [
            {
              id: 1,
              title: '$5.000 - $10.000',
              checked: true,
            },
            {
              id: 2,
              title: '$10.000 - $20.000',
            },
            {
              id: 3,
              title: '$20.000 - $50.000',
            },
            {
              id: 4,
              title: '$50.000 +',
            },
          ],
        },
        box4: {
          img: 'check.svg',
          title: 'Submit your quote request',
          desc: 'Please review all the information you previously typed in the past steps, and if all is okay, submit your message to receive a project quote in 24 - 48 hours.',
        },
      },
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
    onAddData(elem) {
      console.log(elem);
      dataToSend.push(elem);
    },
    assignmentParameterCheckbox() {
      let checkedArray = this.boxs.box2.checkboxs
        .map((item) => (item.checked ? item.title : ''))
        .filter((elem) => elem);
      this.dataToSend.ourServices.push(...checkedArray);
    },
    assignmentParameterRadioButton() {
      let currentBudget = this.boxs.box3.radioButtons
        .map((item) => (item.checked ? item.title : ''))
        .filter((elem) => elem);
      this.dataToSend.projectBudget = currentBudget[0];
    },
    onSentData() {
      localStorage.setItem('dataToSend', JSON.stringify(this.dataToSend));
      console.log('GOOD SENT');
    },
  },
  mounted() {
    this.assignmentParameterCheckbox();
    this.assignmentParameterRadioButton();
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
        <FormSteps :activeStep="activeStep" :numberSteps="numberSteps"></FormSteps>
        <div v-show="activeStep === 1" class="form-box">
          <div class="form-box__title">{{ boxs.box1.title }}</div>
          <div class="form-box__desc">{{ boxs.box1.text }}</div>
          <div class="form-box__items">
            <div v-for="item in boxs.box1.inputs" :key="item.id" class="form-box__item">
              <InputComponent v-bind="item" v-model:contact-details="dataToSend.contactDetails" />
            </div>
          </div>
        </div>
        <div v-show="activeStep === 2" class="form-box">
          <div class="form-box__title">{{ boxs.box2.title }}</div>
          <div class="form-box__desc">{{ boxs.box2.text }}</div>
          <div class="form-box__items">
            <div v-for="item in boxs.box2.checkboxs" :key="item.id" class="form-box__item">
              <Checkbox v-bind="item" v-model:our-services="dataToSend.ourServices" />
            </div>
          </div>
        </div>
        <div v-show="activeStep === 3" class="form-box">
          <div class="form-box__title">{{ boxs.box3.title }}</div>
          <div class="form-box__desc">{{ boxs.box3.text }}</div>
          <div class="form-box__items">
            <div v-for="item in boxs.box3.radioButtons" :key="item.id" class="form-box__item">
              <RadioButton :title="item.title" v-model:project-budget="dataToSend.projectBudget" />
            </div>
          </div>
        </div>
        <FormTotalBox v-if="activeStep === 4" :onSentData="this.onSentData" />
      </form>
      <div class="buttons">
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
