<script setup>
  import Avatar from "./components/Avatar/Avatar.vue";
  import ProfileData from "./components/ProfileData/ProfileData.vue";
  import Password from "./components/Password/Password.vue";
</script>

<template>
  <div class="container">
    <h1 class="home_title">Мой профиль</h1>
    <Avatar/>
    <ProfileData/>
    <Password/>
  </div>
</template>

<style scoped lang="sass">
  .home_title
    text-align: center
    font-size: 56px
    margin-bottom: 20px

  @media (max-width: 1023px)
    .home_title
      font-size: 30px
</style>