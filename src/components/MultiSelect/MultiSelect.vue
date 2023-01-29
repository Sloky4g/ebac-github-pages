<script setup>
  import {ref} from "vue";
  import {Field} from "vee-validate";

  const show = ref(false);
  const selected = ref([]);

  const languages = [
    {
      id: 1,
      title: "Русский",
      name: "ru",
    },
    {
      id: 2,
      title: "Английский",
      name: "en",
    },
    {
      id: 3,
      title: "Япониский",
      name: "jp",
    },
  ]

  const toggle = () => {
    show.value = !show.value;
  }
</script>

<template>
  <div class="multiselect_wrapper">
    <p @click.stop="toggle">
      Владение языками
      <span
          v-if="selected.length"
          v-for="select in selected"
          :key="select"
          class="multiselect_badge"
      >
        {{select}}
      </span>
    </p>
    <div v-show="show">
      <div
          v-for="lang in languages"
          class="multiselect_item"
          :key="lang.id"
      >
        <Field
            name="languages"
            type="checkbox"
            :value="lang.title"
            :id="lang.id"
            v-model="selected"
        />
        <label
            class="multiselect_item-label"
            :for="lang.id"
        >
          {{lang.title}}
        </label>
      </div>
    </div>
  </div>
</template>

<style scoped lang="sass">
  .multiselect_wrapper
    cursor: pointer
    padding: 10px
    border-radius: 10px
    border: 1px solid #ccc
    margin-bottom: 10px

  .multiselect_badge
    margin: 0 10px
    padding: 2px
    font-size: .7rem
    font-weight: 700
    border: 1px solid #ccc
    border-radius: 10px
    background: #eee

  .multiselect_item
    padding: 5px
    display: flex
    input
      cursor: pointer
      margin-right: 10px

  .multiselect_item:hover
    border-radius: 10px
    background: #ccc

  .multiselect_item-label
    cursor: pointer
    display: block
    width: 100%
</style>