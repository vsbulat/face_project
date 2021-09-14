<template>
  <label class="checkbox">
    <input type="checkbox" :value="value" @change="updateInput"/>
    <span class="checkmark"></span>
    {{ label }}
  </label>
</template>
<script>
export default {
  props: {
    "value": {type: [String, Number]},
    "modelValue": {default: []},
    "label": {type: String}
  },
  emits: ['update:modelValue'],
  name: 'app-checkbox',
  data() {
    return {
      //isChecked: false
    }
  },
  methods: {
    updateInput(event) {
     //let isChecked = event.target.checked

      if (this.modelValue.includes(this.value)) {
        let arr = [...this.modelValue];
        arr = arr.filter(item => item !== this.value)
        this.$emit('update:modelValue', arr)
      }
      else {
        this.modelValue.push(this.value)
      }

    }
  }
}
</script>
<style scoped lang="scss">
@import "src/style/variables";

  .checkbox {
    position: relative;
    display: inline-block;
    padding-left: 30px;
    font-weight: normal;
    font-size: 16px;
    line-height: 19px;
    color: $dark_text;

    input,
    .checkmark {
      width: 20px;
      height: 20px;
      position: absolute;
      top: 0;
      left: 0;
      background-color: transparent;
    }

    input {
      z-index: 2;
      opacity: 0;
      cursor: pointer;
      margin: 0;
    }

    .checkmark {
      border: 1px solid $gray;
      border-radius: 6px;
      transition: all, 0.25s;

      &:after {
        content: '';
        width: 12px;
        height: 11px;
        mask-image: url("data:image/svg+xml,%3Csvg width='12' height='10' viewBox='0 0 12 10' fill='none' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M10.7201 1.00109L3.81655 7.72479L1.27994 5.25426C1.15696 5.13448 0.957554 5.13448 0.834544 5.25426L0.0922372 5.97723C-0.0307457 6.09701 -0.0307457 6.29122 0.0922372 6.41103L3.59384 9.82142C3.71682 9.9412 3.91623 9.9412 4.03924 9.82142L11.9078 2.15786C12.0307 2.03808 12.0307 1.84387 11.9078 1.72406L11.1655 1.00109C11.0425 0.88131 10.8431 0.88131 10.7201 1.00109Z' fill='white'/%3E%3C/svg%3E%0A");
        background-color: $white;
        opacity: 0;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        transition: opacity, 0.25s;
      }
    }

    input:checked + .checkmark {
      background-color: $main;
      border-color: $main;

      &:after {
        opacity: 1;
      }
    }
  }
</style>