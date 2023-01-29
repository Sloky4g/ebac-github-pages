<script setup>
  import {defineEmits} from "vue";

  const emit = defineEmits(["uploadAvatar"]);

  const uploadAvatar = (e) => {
    emit("uploadAvatar", e);
  }
</script>

<template>
  <div>
    <input
        class="input input_file"
        id="input_file"
        type="file" name="file"
        accept="image/*"
        @change="uploadAvatar"
    />
    <label for="input_file" class="input_file-button">
      <span class="input_file-icon_wrapper">+</span>
      <span class="input_file-button_text">Выберите файл</span>
    </label>
  </div>
</template>

<style scoped lang="sass">
  .input_file
    width: 0
    opacity: 0
    visibility: hidden
    position: absolute

  .input_file-button
    height: 40px
    width: 100%
    background: #1b53bc
    color: #fff
    display: flex
    justify-content: flex-start
    gap: 10px
    cursor: pointer

  .input_file-button:hover
    background: #174191

  .input_file-icon_wrapper
    padding: 0 20px
    display: flex
    align-items: center
    font-size: 1.1rem
    font-weight: 700
    border-right: 1px solid #fff

  .input_file-button_text
    padding: 0 10px
    display: flex
    align-items: center
    font-size: 1.125rem
    font-weight: 700
</style>