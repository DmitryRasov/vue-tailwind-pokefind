<template>
  <div class="modal" v-if="show" @click.stop="hideModal" @hideModal="$emit('hideModal', this.show)">
    <div @click.stop class="modal__content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModalWindow",
  props: {
    show: {
      type: Boolean,
      default: false,
    }
  },
  methods: {
    hideModal(){
      this.$emit('update:show', false)
    }
  }
}
</script>

<style scoped>
.modal {
  display: flex;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(255, 255, 255, 0.01);
  backdrop-filter: blur(2px);
}
.modal__content {
  margin: auto;
  background: #FFFFFF;
  border: 1px solid #DDE2E4;
  border-radius: 6px;
  width: 25em;
  height: 17.5em;
  box-shadow: 0px 25px 50px -12px #00000040;

}
</style>