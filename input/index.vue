<template>
  <div class="form__item">
    <label :for="name" :class="{'required': $attrs.required}">{{ label }}</label>
    <textarea
      v-if="type === 'textarea'"
      v-bind="$attrs"
      :id="name"
      :value="value"
      @input="onInput">
    </textarea>
    <select
      v-else-if="type === 'select'"
      v-bind="$attrs"
      :value="value"
      @change="onSelectChange">
      <option
        v-for="option in options"
        :key="option.value"
        :value="option.value"
        :disabled="option.disabled">
        {{ option.label }}
      </option>
    </select>
    <template
      v-else-if="type === 'radio'"
      v-for="radio in options">
      <input
        type="radio"
        :id="radio.name"
        :key="radio.value"
        :name="name"
        :value="radio.value"
        @change="onRadioChange"
        v-bind="$attrs">
      <label
        :for="radio.name"
        :key="radio.name">
        {{ radio.label }}
      </label>
    </template>
    <input
      v-else
      v-bind="$attrs"
      :type="type"
      :id="name"
      :value="value"
      @input="onInput">
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: ['label', 'value', 'name', 'type', 'options'],
  inheritAttrs: false,
  methods: {
    onInput(e) {
      this.$emit('input', e.target.value)
    },
    onSelectChange(e) {
      this.$emit('selectChange', e.target.value)
    },
    onRadioChange(e) {
      this.$emit('radioChange', e.target.value)
    }
  }
}
</script>

<style lang="scss">
$theme-color: #FF5A00;
.form__item {
  height: 40px;
  margin-bottom: 30px;
  line-height: 40px;
  font-size: 0;
  label {
    display: inline-block;
    margin-right: 19px;
    font-size: 14px;
    &:first-child {
      margin-right: 0;
      min-width: 80px;
    }
  }
}
label.required::after {
  content: '*';
  display: inline-block;
  margin-right: 16px;
  color: $theme-color;
}
&.form__sex {
  display: inline-block;
  position: relative;
  input[type="radio"] {
    position: absolute;
    top: 12px;
    opacity: 0;
  }
  #name {
    width: 160px;
    margin-right: 16px;
  }
}
&.form__name {
  display: inline-block;
  margin-right: 36px;
  &.input__short {
    & + .form__sex {
      label {
        min-width: auto;
        &:first-child {
          width: 0;
          &::after {
            content: ''
          }
        }
      }
    }
    input {
      width: 160px;
    }
  }
}
&.form__description {
  height: auto;
}
input[type="text"], input[type="tel"], input[type="password"] {
  display: inline-block;
  width: 330px;
  padding: 13px 9px;
  font-size: 14px;
  border: 1px solid #dddddd;
  border-radius: 8px;
  box-sizing: border-box;
  &:focus {
    outline: 0;
    box-shadow: 0px 0px 3px $theme-color;
    border-color: $theme-color;
  }
}

input::-webkit-input-placeholder, textarea::-webkit-input-placeholder {
  color: #B2B2B2;
}

input:-ms-input-placeholder, textarea:-ms-input-placeholder {
  color: #B2B2B2;
}

select {
  position: relative;
  width: 330px;
  padding: 13px 9px;
  font-size: 14px;
  line-height: 0;
  border: 1px solid #dddddd;
  border-radius: 8px;
  box-sizing: border-box;
  &:focus {
    outline: 0;
    box-shadow: 0px 0px 3px $theme-color;
    border-color: $theme-color;
  }
}

textarea {
  width: 840px;
  height: 180px;
  padding: 13px 9px;
  font-size: 14px;
  border-radius: 8px;
  border: 1px solid #dddddd;
  vertical-align: middle;
  &:focus {
    outline: 0;
    box-shadow: 0px 0px 3px $theme-color;
    border-color: $theme-color;
  }
}

input[type="radio"] + label::before{
  position: relative;
  top: -2px;
  content: '';
  display: inline-block;
  width: 16px;
  height: 16px;
  margin-right: 8px;
  transition: all .2s ease;
  border-radius: 50%;
  border: 1px solid #ddd;
  box-sizing: border-box;
  vertical-align: middle;
}

input[type="radio"]:checked + label::before{
  border: 4.5px solid $theme-color;
}

</style>
