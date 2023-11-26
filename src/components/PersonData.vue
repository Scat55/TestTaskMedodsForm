<script setup>
import { ref, computed } from 'vue'
import useVuelidate from '@vuelidate/core';
import { maxLength, minLength, required, helpers, numeric } from '@vuelidate/validators'
import Input from '@/components/Input.vue'


const nameField = ref('')
const lastNameField = ref('')
const birthdayFiled = ref('')
const numberFiled = ref(7)
const patronymicField = ref('')

const rules = computed(() => ({
  lastNameField: {
    required: helpers.withMessage(`Обязательное поле`, required)
  },
  nameField: {
    required: helpers.withMessage(`Обязательное поле`, required)
  },
  birthdayFiled: {
    required: helpers.withMessage(`Обязательное поле`, required)
  },
  numberFiled: {
    required: helpers.withMessage(`Обязательное поле`, required),
    numeric: helpers.withMessage(`Вы можете вводить только цифры`, numeric),
    maxLength: helpers.withMessage(`Максимальная длинна 11 символов`, maxLength(11)),
    minLength: helpers.withMessage(`Минимальная длинна 11 символов`, minLength(11)),
  },
}))
const v = useVuelidate(rules, { nameField, lastNameField, birthdayFiled, numberFiled, patronymicField })

</script>
<template>
  <div class="container">
    <form class="form">
      <Input
        type="text"
        label="Ваше имя*"
        name="name"
        placeholder="Введите ваше имя"
        v-model:value="v.nameField.$model"
        :error="v.nameField.$errors"
      />
      <Input
        type="text"
        label="Ваша фамилия*"
        name="lastname"
        placeholder="Введите вашу фамилию"
        v-model:value="v.lastNameField.$model"
        :error="v.lastNameField.$errors"
      />
      <Input
        type="text"
        label="Ваш отчество"
        name="patronymic"
        placeholder="Введите ваше отчество"
        v-model:value="patronymicField"
      />
      <Input
        type="date"
        label="Дата рождения*"
        name="Email"
        placeholder="Введите вашу дату рождения"
        v-model:value="v.birthdayFiled.$model"
        :error="v.birthdayFiled.$errors"
      />
      <Input
        type="number"
        label="Ваша номер телефона*"
        name="number"
        placeholder="Введите ваш номер телофона"
        v-model:value="v.numberFiled.$model"
        :error="v.numberFiled.$errors"
      />

    </form>
  </div>
</template>



<style lang="sass" scoped>
.form
  display: flex
  gap: 1rem
  align-items: center
  flex-wrap: wrap
  margin-top: 2rem
  margin-left: 1rem
</style>