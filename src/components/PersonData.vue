<script setup>
import { ref, computed } from 'vue'
import useVuelidate from '@vuelidate/core';
import { minLength, email, helpers } from '@vuelidate/validators'
import Input from '@/components/Input.vue'


const emailField = ref('')

const rules = computed(() => ({
  emailField: {
    email: helpers.withMessage(`Неккоректный email`, email)
  }
}))
const v = useVuelidate(rules, { emailField })
console.log(v)
</script>
<template>
  <form>
    <Input
      type="email"
      label="Ваша почта"
      name="Email"
      placeholder="Введите ваш email"
      v-model:value="v.emailField.$model"
      :error="v.emailField.$errors"
    />
  </form>
</template>



<style lang="sass" scoped>
form
  margin-top: 2rem
  margin-left: 1rem
</style>