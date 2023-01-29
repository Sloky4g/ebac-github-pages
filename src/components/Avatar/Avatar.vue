<script setup>
  import {ref} from "vue";
  import FileInput from "../FileInput/FileInput.vue";

  let image = ref(null);

  const uploadAvatar = (e) => {
    let files = e.target.files || e.dataTransfer.files;
    if (files.length) {
      const reader = new FileReader();

      reader.onload = function (e) {
        image.value = e.target.result;
      }

      reader.readAsDataURL(files[0]);
    }
  }

  const deleteAvatar = () => {
    image.value = null;
  }
</script>

<template>
  <div class="avatar-container">
    <h2 class="avatar-title">Изменение аватара</h2>
    <div class="avatar-img_container">
      <img v-if="image === null" src="../../../public/no-img.jpg" alt="no-avatar-img">
      <img v-else v-bind:src="image" alt="avatar-img" class="avatar_img">
    </div>
    <div>
      <FileInput @uploadAvatar="uploadAvatar" @deleteAvatar="deleteAvatar"/>
    </div>
    <button class="base_styled_btn" @click="deleteAvatar">Удалить аватар</button>
  </div>
</template>

<style scoped lang="sass">
  .avatar-container
    margin-bottom: 30px
    max-width: 250px
    max-height: 450px
    display: flex
    flex-direction: column
    justify-content: space-between
    gap: 20px

  .avatar-title
    margin-bottom: 20px

  .avatar-img_container
    img
      width: 100%
      height: auto
      
  @media (max-width: 1023px)
    .avatar-container
      text-align: center
      margin: 0 auto 30px
</style>