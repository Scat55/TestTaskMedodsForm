<script setup>
const emit = defineEmits(['update:value'])
const props = defineProps({
  error: {
    type: Array,
    required: false
  },
  value: {
    type: String,
    default: ''
  },
  name: {
    type: String,
    required: true
  },
  type: {
    type: String,
    default: 'text'
  },
  placeholder: {
    type: String,
    required: true
  },
  label: {
    type: String,
    required: true
  },
  width: {
    type: String,
    default: '300px'
  }
})

const updateValue = (e) => {
  emit('update:value', e.target.value)
}
</script>

<template>
  <div
    class="form-input"
    :style="{ width: width }"
  >
    <input
      class="input-text"
      :type="type"
      :name="name"
      :id="name"
      :placeholder="placeholder"
      :value="value"
      @input="updateValue"
    >
    <label
      :for="name"
      class="input-label"
    >{{ label }}</label>
    <TransitionGroup>
      <div
        class="form-error"
        v-for="element of error"
        :key="element.$uid"
      >
        <div class="form-error__message">{{ element.$message }}</div>
      </div>
    </TransitionGroup>
  </div>
</template>



<style lang="sass" scoped>
.form-input 
    margin-bottom: 1.875rem
    position: relative
.form-error 
  background: var(--danger)
  margin-top: .25rem
  border-radius: .4375rem
  font-size: .8125rem
  color: #fff
  padding: .3125rem
  

.input-text 
  border: 1px solid var(--primary)
  padding: 0 .625rem
  height: 2.5rem
  border-radius: .4375rem
  font-size: .9375rem
  width: 100%
  position: relative
  z-index: 1
  &:focus 
    & + .input-label 
      z-index: 1
      opacity: 1
      top: -1.25rem

    &:not(:placeholder-shown) 
      & + .input-label 
        z-index: 1
        opacity: 1
        top: -1.25rem

.input-label 
  font-weight: bold
  display: block
  position: absolute
  top: 1.25rem
  opacity: 0
  z-index: -1
  transition: .3s
  font-size: .8125rem
  color: var(--primary)

.v-enter-active,
.v-leave-active 
  transition: opacity 0.5s ease

.v-enter-from,
.v-leave-to 
  opacity: 0

</style>