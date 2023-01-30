<template>
  <div class="Modal" v-if="show">
    <div class="Modal--content">
      <div class="Modal--close" 
      @click="CloseButtonClick"></div>
      <slot></slot>
    </div>
  </div>
</template>
<script>
import feather from "feather-icons";
export default {
  name: "ModalSvg",
  props: {
    show: {
      typer: Boolean,
      default: "false",
    },
  },
  computed: {
    closeIcon() {
      return feather.icons.circle.toSvg();
      
    },
  },

  methods: {
    CloseButtonClick() {
      this.$emit("onCancelClick");
    },
  },
};
</script>
<style lang="less" scoped>
.Modal {
  // background: rgba(0, 0, 0, 0.4);
  // position: fixed;
  // width: 100%;
  // height: 100%;
  // top: 0;
  // left: 0;
  &--content {
    background-color: rgba(241, 241, 241, 0.9);
    // position: fixed;
    width: 100%;
    padding: 30px;
    top: 15vh;
    height: 55vh;
  }
}
</style>
