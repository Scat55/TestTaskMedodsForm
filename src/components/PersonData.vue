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
const genderField = ref('Пол')

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


const handler = () => {
  v.value.$touch() // Проверка на ошибки

  if (v.value.$error) return

  alert('Успешно')
  console.log(nameField.value, lastNameField.value, patronymicField.value, birthdayFiled.value, numberFiled.value, genderField.value)

}

</script>
<template>
  <div class="container">
    <form
      class="form"
      @submit.prevent="handler"
    >
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
        label="Ваше отчество"
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
        label="Ваш номер телефона*"
        name="number"
        placeholder="Введите ваш номер телофона"
        v-model:value="v.numberFiled.$model"
        :error="v.numberFiled.$errors"
      />

      <select
        name="gender"
        class="select"
        v-model="genderField"
        @click="test"
      >
        <option
          value="Пол"
          disabled
        >Ваш пол</option>
        <option value="Мужской">Мужской</option>
        <option value="Женский">Женский</option>
      </select>

      <button
        class="btn"
        type="submit"
      >Далее</button>
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

.select
  border: 1px solid var(--primary)
  padding: 0 0.625rem
  height: 2.5rem
  border-radius: 0.4375rem
  font-size: 0.9375rem
  width: 18.75rem
  align-self: flex-start

.btn
  justify-self: flex-end
  align-self: flex-end
  background-color: var(--primary)
  color: #fff
  padding: .625rem 1.25rem
  border-radius: 0.5rem
  border: none
  outline: none
  cursor: pointer
  transition: all .3s

  &:hover
    background-color: lighten(#6979f8, 3% )
</style>