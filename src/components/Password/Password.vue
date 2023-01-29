<script setup>
  import {Form, defineRule} from "vee-validate";
  import {ref} from "vue";
  import FormInput from "../FormInput/FormInput.vue";

  const password = ref("Testpass123");

  const onSubmit = (values) => {
    password.value = values.newPassword1;
  }

  // Validation Rules

  defineRule("oldPasswordValidation", (value) => {
    if (value !== password.value) {
      return "Введен неправильный текущий пароль"
    }

    return true;
  })

  const passwordValidation = (value) => {
    const regex = /(?=.*[0-9])(?=.*[a-z])(?=.*[A-Z])[0-9a-zA-Z!@#$%^&*]{6,}/g
    if (!regex.test(value)) {
      return "Пароль должен содержать хотя бы одну латинскую букву в нижнем регистре, одну в верхнем регистре, одну цифру и состоять не менее, чем из 6 символов"
    }

    return true;
  }

  defineRule("required", (value) => {
    if (!value) {
      return "Поле не может быть пустым";
    }

    return true;
  });

  defineRule("passwordValidation", passwordValidation);

  defineRule("confirmed", (value, [target], ctx) => {
    if (value === ctx.form[target]) {
      return true;
    }

    return "Поля с новым паролем и подтвержденным паролем должны совпадать"
  })

  defineRule("uniqPassword", (value, [target], ctx) => {
    if (value === ctx.form[target]) {
      return "Новый пароль должен отличаться от старого"
    }
    return true;
  })
</script>

<template>
  <div class="password-container">
    <h2 class="password-title">Изменение пароля</h2>
    <p class="password-text">Текущий пароль: {{password}}</p>
    <Form @submit="onSubmit" class="password-form">
      <FormInput
          label-title="Текущий пароль"
          required="true"
          name="oldPassword"
          placeholder="Введите текущий пароль"
          type="password"
          rules="required|oldPasswordValidation"
      />
      <FormInput
          label-title="Новый пароль"
          required="true"
          name="newPassword1"
          placeholder="Введите новый пароль"
          type="password"
          rules="required|passwordValidation"
      />
      <FormInput
          label-title="Подтверждение пароля"
          required="true"
          name="newPassword2"
          placeholder="Введите новый пароль еще раз"
          type="password"
          rules="required|confirmed:newPassword1|uniqPassword:oldPassword|passwordValidation"
      />
      <button>Изменить пароль</button>
    </Form>
  </div>
</template>

<style scoped lang="sass">
  .password-container
    margin-bottom: 30px

  .password-title
    margin-bottom: 20px

  .password-text
    margin-bottom: 20px

  .password-form
    width: 40%

  @media (max-width: 767px)
    .password-form
      width: 100%
      margin: 0 auto 30px
</style>