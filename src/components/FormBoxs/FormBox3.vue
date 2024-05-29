<script>
import RadioButton from '../UI/RadioButton.vue';
export default {
  props: {
    projectBudget: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      box: {
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
    };
  },
  components: {
    RadioButton,
  },
  methods: {
    assignmentParameterRadioButton() {
      let currentBudget = this.box.radioButtons
        .map((item) => (item.checked ? item.title : ''))
        .filter((elem) => elem);
      this.$emit('update:projectBudget', currentBudget[0]);
    },
    changeCurrentBudget(elem) {
      this.$emit('update:projectBudget', elem);
    },
  },
  mounted() {
    this.assignmentParameterRadioButton();
  },
};
</script>

<template>
  <div class="form-box">
    <div class="form-box__title">{{ box.title }}</div>
    <div class="form-box__desc">{{ box.text }}</div>
    <div class="form-box__items">
      <div v-for="item in box.radioButtons" :key="item.id" class="form-box__item">
        <RadioButton
          :title="item.title"
          @projectBudget="changeCurrentBudget"
          :projectBudget="this.projectBudget"
        />
      </div>
    </div>
  </div>
</template>

<style></style>
