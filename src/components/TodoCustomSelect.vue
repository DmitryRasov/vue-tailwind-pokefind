<template>
  <div>
    <p></p>
    <div class="options">
      <p
        v-for="option in options"
        :key="option.value"
      >
        {{ option.name }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "TodoCustomSelect",
  props: {
    options: {
      type: Array,
      default: () => []
    }
  },
  data(){
    return{

    }
  }
}
</script>

<style>

</style>