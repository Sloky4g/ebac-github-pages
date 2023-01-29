<script setup>
  import {defineProps} from "vue";

  const {profileData} = defineProps(["profileData"]);
</script>

<template>
  <div class="profile-content-info">
    <div class="profile-content-info-item">
      <p class="profile-content-info-item-title">ФИО:</p>
      <p v-if="profileData.name">{{profileData.name}}</p>
      <p v-else>Нет данных</p>
    </div>
    <div class="profile-content-info-item">
      <p class="profile-content-info-item-title">Дата рождения:</p>
      <p v-if="profileData.birthday">{{profileData.birthday}}</p>
      <p v-else>Нет данных</p>
    </div>
    <div class="profile-content-info-item">
      <p class="profile-content-info-item-title">E-mail:</p>
      <p v-if="profileData.city">{{profileData.city}}</p>
      <p v-else>Нет данных</p>
    </div>
    <div class="profile-content-info-item">
      <p class="profile-content-info-item-title">Город:</p>
      <p v-if="profileData.email">{{profileData.email}}</p>
      <p v-else>Нет данных</p>
    </div>
    <div class="profile-content-info-item">
      <p class="profile-content-info-item-title">Телефон:</p>
      <p v-if="profileData.code && profileData.phone">{{profileData.code}}{{profileData.phone}}</p>
      <p v-else>Нет данных</p>
    </div>
    <div class="profile-content-info-item">
      <p class="profile-content-info-item-title">Языки:</p>
      <div>
        <p v-if="profileData.languages.length" v-for="lang in profileData.languages">{{lang}}</p>
        <p v-else>Нет данных</p>
      </div>
    </div>
  </div>
</template>

<style scoped lang="sass">
  .profile-content-info
    border: 1px solid #ccc
    border-radius: 10px
    padding: 10px
    width: 40%
    height: 100%

  .profile-content-info-item
    display: flex
    gap: 10px
    margin-bottom: 10px

  .profile-content-info-item-title
    width: 150px

  .profile-content-info-item:last-child
    margin-bottom: 0

  @media (max-width: 767px)
    .profile-content-info
      width: 100%
</style>