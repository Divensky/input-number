<script lang="ts">
import { defineComponent, PropType, ref, computed, watch } from 'vue';
import { classname } from '../../../utils/classname';
import { allowedKeys } from './allowedKeys';

type InputQuery = string | number | null;

export default defineComponent({
  name: 'BaseInputNumber',
  props: {
    noBorder: {
      type: Boolean,
      default: false,
    },
    modelValue: {
      type: [String, Number] as PropType<InputQuery>,
      default: null,
    },
    size: {
      type: String as PropType<'sm'>,
      default: null,
    },
    hideSpinner: {
      type: Boolean,
      default: false,
    },
    hideErrors: {
      type: Boolean,
      default: false,
    },
  },
  emits: ['update:model-value'],
  setup(props, { emit }) {
    const inputQuery = ref<InputQuery>(null);
    const errorMessage = ref('');
    watch(inputQuery, (newValue) => {
      emit('update:model-value', newValue);
      if (errorMessage.value && typeof newValue === 'number') {
        errorMessage.value = '';
      }
    });
    watch(
      () => props.modelValue,
      (newValue) => (inputQuery.value = newValue),
      { immediate: true }
    );

    const onKeypress = (e: KeyboardEvent) => {
      if (!allowedKeys.includes(e.key) && !props.hideErrors) {
        errorMessage.value = 'Please enter a number';
      }
    };
    const errors = computed(() => {
      return errorMessage.value
        ? { error: true, 'error-message': errorMessage.value }
        : null;
    });
    const clearError = () => {
      errorMessage.value = '';
    };

    return {
      inputQuery,
      cn: classname('base-input'),
      errorMessage,
      onKeypress,
      errors,
      clearError,
    };
  },
});
</script>

<template>
  <q-input
    v-model.number="inputQuery"
    type="number"
    outlined
    :class="cn({ size: size, 'no-border': noBorder })"
    :input-class="cn('input', { 'hide-spinner': hideSpinner })"
    v-bind="errors"
    bottom-slots
    @keyup="onKeypress"
    @keydown.delete="clearError"
  >
    <template #append>
      <slot name="append"></slot>
    </template>
  </q-input>
</template>

<style lang="scss">
.base-input {
  &__input {
    &_hide-spinner {
      -moz-appearance: textfield;
      appearance: textfield;

      &::-webkit-inner-spin-button,
      &::-webkit-outer-spin-button {
        -webkit-appearance: none;
      }
    }
  }
}
</style>
