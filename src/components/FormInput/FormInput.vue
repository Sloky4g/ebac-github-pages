<script setup>
  import {Field, ErrorMessage} from "vee-validate";
  import {defineProps} from "vue";

  const props = defineProps([
    "labelTitle",
    "required",
    "name",
    "placeholder",
    "type",
    "rules",
    "style",
  ]);
</script>

<template>
  <div class="input_wrapper">
    <label class="input_label" :for="props.name">
      {{props.labelTitle}}
      <span v-if="props.required">*</span>
    </label>
    <Field
        :style="props.style"
        class="input"
        :name="props.name"
        :placeholder="props.placeholder"
        :rules="props.rules"
        :type="props.type"
    />
    <ErrorMessage class="input-error" :name="props.name"/>
  </div>
</template>

<style scoped lang="sass">
  .input_wrapper
    margin-bottom: 10px
    display: flex
    flex-direction: column

  .input_label
    span
      color: #e31d1d

  .input
    padding: 10px
    border-radius: 10px
    border: 1px solid #ccc
    width: 100%

  .input-error
    color: #e31d1d
    padding: 0 10px
    font-size: .9rem
</style>