<template>
  <select class="select" v-model="modelValue" @change="changeOption">
    <option disabled value="">Выбрать</option>
    <option v-for="option in options"
            :key="option.value"
            :value="option.value"
    >
      {{ option.name }}
    </option>
  </select>
</template>

<script>
export default {
  name: "TodoSelect",
  props: {
    modelValue: {
      type: String
      },
    options: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    changeOption(event){
      this.$emit('update:modelValue', event.target.value)
    }
  }
}
</script>

<style scoped>
.select {
  border: none;
  width: 5em;
  font-size: 1em;
  margin-left: .5em;
}
</style>