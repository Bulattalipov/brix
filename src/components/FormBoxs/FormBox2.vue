<script>
import Checkbox from '../UI/Checkbox.vue';
export default {
  props: {
    ourServices: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      box: {
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
    };
  },
  components: {
    Checkbox,
  },
  methods: {
    assignmentParameterCheckbox() {
      if (this.ourServices.length === 0) {
        let checkedArray = this.box.checkboxs
          .map((item) => (item.checked ? item.title : ''))
          .filter((elem) => elem);
        this.ourServices.push(...checkedArray);
      }
    },
    changeOurServices(elem) {
      this.$emit('update:ourServices', elem);
    },
  },
  mounted() {
    this.assignmentParameterCheckbox();
  },
};
</script>

<template>
  <div class="form-box">
    <div class="form-box__title">{{ box.title }}</div>
    <div class="form-box__desc">{{ box.text }}</div>
    <div class="form-box__items">
      <div v-for="item in box.checkboxs" :key="item.id" class="form-box__item">
        <Checkbox v-bind="item" @ourServices="this.changeOurServices" :our-services="ourServices" />
      </div>
    </div>
  </div>
</template>

<style></style>
