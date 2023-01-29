<script setup>
  import {Field} from "vee-validate";

  const vCodeMask = {
    mounted: function (el, binding) {
      el.value = binding.value;
      el.addEventListener("click", function() {
        el.setSelectionRange(el.value.length,el.value.length);
      })
      el.addEventListener("input", function() {
        if (el.value === "") {
          el.value = "+";
        }
      })
    }
  }

  const vMask = {
    mounted: function (el, binding) {
      let mask = binding.value;
      let first = mask.indexOf("_");
      let clean = mask.replace(/[^0-9_]/gm, "");
      let indexes = [];

      for (let i = 0; i < clean.length; i++) {
        if (!isNaN(clean[i])) {
          indexes.push(i);
        }
      }

      el.value = mask;
      el.clean = mask.replace(/[^0-9]/gm, "");

      const maskIt = () => {
        let value = el.value;
        let filtered = value.replace(/[^0-9]/gm, "");
        let result = "";

        if (value.length < first) {
          value = mask + value;
          filtered = value.replace(/[^0-9]/gm, "");
        }

        for (let i = 0; i < filtered.length; i++) {
          if (indexes.indexOf(i) === -1) {
            result += filtered[i];
          }
        }

        value = "";
        let cursor = 0;

        for (let i = 0; i < mask.length; i++) {
          if (mask[i] === "_" && result) {
            value += result[0];
            result = result.slice(1);
            cursor = i + 1;

          } else {
            value += mask[i];
          }
        }

        if (cursor < first) {
          cursor = first;
        }

        el.value = value;

        el.clean = el.value.replace(/[^0-9]/gm, "");

        el.setSelectionRange(cursor, cursor);
      }

      el.addEventListener("focus", function(event) {
        event.preventDefault();
      })

      el.addEventListener("click", function(event) {
        event.preventDefault();
        let start = el.value.indexOf("_");

        if (start === -1) {
          start = el.value.length;
        }

        el.setSelectionRange(start,start);
      })

      el.addEventListener("paste", function() {
        let start = el.selectionStart;

        if (start < first) {
          el.value = "_" + el.value;
        }
      })

      el.addEventListener("input", function() {
        maskIt();
      })
    }
  }
</script>

<template>
  <div class="input_wrapper">
    <label for="phone">Телефон</label>
    <div class="input_container">
      <Field
          class="phone_input country_input"
          name="code"
          v-code-mask="'+'"
      />
      <Field
          class="phone_input phone_input"
          name="phone"
          v-mask="'(___) ___ __ __'"
      />
    </div>
  </div>
</template>

<style scoped lang="sass">
  .input_wrapper
    margin-bottom: 10px
    display: flex
    flex-direction: column

  .phone_input
    padding: 10px
    border-radius: 10px
    border: 1px solid #ccc
    
  .input_container
    display: flex
    gap: 10px

  .country_input
    width: 50px
</style>