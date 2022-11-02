<template>
  <v-form ref="form" v-model="valid" @submit.prevent="onSearch">
    <label class="mb-1">{{label}}</label>
    <v-text-field
      v-model="search"
      :placeholder="placeholder"
      :prefix="prefix"
      :type="type"
      :suffix="suffix"
      :variant="variant"     
      hide-details="auto"
      :clearable="clearable"
      :counter="counter"
      :color="color"
      :bg-color="bgColor"
      :density="density"
      :disabled="disabled"
      :focused="focused"
      :autofocus="autofocus"
      :loading="loading"
      :reverse="reverse"
      :readonly="readonly"
      :single-line="singleLine"
      :persistent-clear="persistentClear"
      :persistent-counter="persistentCounter"
      :persistent-hint="persistentHint"
      :persistent-placeholder="persistentPlaceholder"
      :hint="hint"
      :rules="rules"
      @input="changeSearch"
    >
      <template #append-inner>
        <v-icon @click="onSearch">
          mdi-magnify
        </v-icon>
      </template>
    </v-text-field>
  </v-form>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { Ref } from 'vue'

type Density = 'default' | 'comfortable' | 'compact'
type Variant = 'underlined' | 'outlined' | 'filled' | 'solo' | 'plain'
type ValidationResult = string | boolean;
type ValidationRule = ValidationResult | PromiseLike<ValidationResult> | ((value: any) => ValidationResult) | ((value: any) => PromiseLike<ValidationResult>)

const props = withDefaults(defineProps<{
  searchDefault?: string,
  label?: string,
  placeholder?: string,
  color?: string,
  bgColor?: string,
  hint?: string,
  prefix?: string,
  type?: string,
  suffix?: string,
  clearable?: boolean,
  disabled?: boolean,
  focused?: boolean,
  autofocus?: boolean,
  loading?: boolean,
  readonly?: boolean,
  reverse?: boolean,
  singleLine?: boolean,
  persistentClear?: boolean,
  persistentCounter?: boolean,
  persistentHint?: boolean,
  persistentPlaceholder?: boolean,
  counter?: string | number | true,
  density?: Density,
  variant?: Variant,
  rules?: ValidationRule[]
}>(), {
  type: 'text',
  searchDefault: '',
  clearable: false,
  disabled: false,
  focused: false,
  autofocus: false,
  loading: false,
  readonly: false,
  reverse: false,
  singleLine: false,
  persistentClear: false,
  persistentCounter: false,
  persistentHint: false,
  persistentPlaceholder: false,
  density: 'compact',
  variant: 'outlined'
})

const emit = defineEmits<{
  (e: 'change', value: string): void
  (e: 'search', value: string): void
}>()

const search: Ref<string> = ref(props.searchDefault)
const valid: Ref<boolean> = ref(true)
  const form = ref<HTMLFormElement>()
  
const changeSearch = async () => {
  if (search.value.trim().length > 0) {
    await form.value?.validate()
    if(valid.value) {
      emit('change', search.value.trim())
    }
  }
}

const onSearch = async () => {
  if (search.value.trim().length > 0) {
    await form.value?.validate()
    if(valid.value) {
      emit('search', search.value.trim())
    }
  }
}
</script>
