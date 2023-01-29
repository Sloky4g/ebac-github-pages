<script setup>
  import {ref} from "vue";
  import {Form} from "vee-validate";
  import FormInput from "../FormInput/FormInput.vue";
  import PhoneInput from "../PhoneInput/PhoneInput.vue";
  import MultiSelect from "../MultiSelect/MultiSelect.vue";
  import ProfileInfo from "../ProfileInfo/ProfileInfo.vue";

  const profileData = ref({
    birthday: "",
    city: "",
    code: "",
    email: "",
    languages: [],
    name: "",
    phone: "",
  });

  const onSubmit = (values) => {
    profileData.value = values;
  }

  // Validation rules
  const isRequired = (value) => {
    if (!value) {
      return "Поле не может быть пустым";
    }
    return true;
  }

  const emailValidation = (value) => {
    if (!value) {
      return "Поле не может быть пустым";
    }

    const regex = /^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$/;
    if (!regex.test(value)) {
      return "Ошибка в написании e-mail"
    }

    return true
  }
</script>

<template>
  <div class="profile-container">
    <h2 class="profile-title">Персональная информация</h2>
    <div class="profile-content">
      <Form @submit="onSubmit" class="profile-form">
        <FormInput
            labelTitle="ФИО"
            required="true"
            name="name"
            placeholder="Введите полное имя"
            type="text"
            :rules="isRequired"
        />
        <FormInput
            style="width: 150px"
            labelTitle="Дата рождения"
            name="birthday"
            type="date"
        />
        <FormInput
            labelTitle="E-mail"
            required="true"
            name="email"
            placeholder="Введите почту"
            type="email"
            :rules="emailValidation"
        />
        <FormInput
            labelTitle="Город"
            name="city"
            placeholder="Введите город"
            type="text"
        />
        <PhoneInput/>
        <MultiSelect/>
        <button>Сохранить</button>
      </Form>
      <ProfileInfo :profileData="profileData"/>
    </div>
  </div>
</template>

<style scoped lang="sass">
  .profile-container
    margin-bottom: 30px

  .profile-title
    margin-bottom: 20px

  .profile-content
    display: flex
    gap: 30px

  .profile-form
    width: 40%

  @media (max-width: 767px)
    .profile-title
      text-align: center

    .profile-content
      flex-direction: column
      align-items: center

    .profile-form
      width: 100%
</style>