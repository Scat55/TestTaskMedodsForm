<script setup>
import { ref, computed } from 'vue'
import useVuelidate from '@vuelidate/core';
import { minLength, email, helpers } from '@vuelidate/validators'


const emaill = ref('')

const rules = computed(() => ({
  emaill: {
    email: helpers.withMessage(`Неккоректный email`, email)
  }
}))
const v = useVuelidate(rules, { emaill })
console.log(v)
</script>
<template>
  <div>

    <input
      type="email"
      placeholder="Ваш email"
      class="input"
      v-model="v.emaill.$model"
    >

    <div
      v-for="error in v.emaill.$errors"
      :key="error.$uid"
      class="error"
    >{{ error.$message }}</div>

  </div>
</template>



<style lang="sass" scoped>
.input
  display: block
  padding: .625rem
  margin-top: 1rem
  margin-left: 1rem
  border-radius: 0.5rem

.error
  display: inline-block
  background-color: #FE5B72
  margin-top: .25rem
  border-radius: .4375rem
  font-size: .8125rem
  color: #fff
  padding: .3125rem
  margin-left: 1rem

</style>