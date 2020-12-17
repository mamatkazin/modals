<template>
  <transition name="modal">
    <div class="modal__wrapper" @click="$emit('close')">
      <div class="modal-content" @click.stop="">
        <div class="modal-header">
          <span class="modal-title font-bold text-xl"> {{ title }} </span>
          <span class="button-close" @click="$emit('close')"></span>
        </div>
        <div class="modal-body">
          <slot name="body">default body</slot>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
  },
  data() {
    return {};
  },
  mounted() {
    document.body.addEventListener("keyup", (e) => {
      if (e.keyCode === 27) {
        this.$emit("close");
      }
    });
  },
  computed: {},
  methods: {},
};
</script>

<style lang="scss" scoped>
// Animation
.modal-enter {
  opacity: 0;
}
.modal-leave-active {
  opacity: 0;
}
.modal-enter .modal-content,
.modal-leave-active .modal-content {
  transform: scale(1.2);
}

.modal__wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  transition: opacity 0.2s ease;
  right: 0;
  z-index: 998;
  background-color: rgba(00, 00, 00, 0.48);
}

.modal-content {
  position: relative;
  max-width: 600px;
  padding: 20px 18px;
  background-color: #fff;
  border: 1px solid #dcdfe6;
  transition: all 0.2s ease;
  border-radius: 8px;
  z-index: 999;
  overflow: hidden;
  @media screen and (min-width: 900px) {
    min-width: 500px;
  }
}
.modal-header {
  display: flex;
  align-self: center;
  justify-content: space-between;
  padding-bottom: 20px;
  span {
    font-size: 24px;
  }
  .button-close {
    position: relative;
    width: 24px;
    height: 24px;
    overflow: hidden;
    opacity: 0.7;
    -webkit-transition: mainTransition;
    -o-transition: mainTransition;
    transition: mainTransition;
    display: inline-block;
    cursor: pointer;
  }

  .button-close:after {
    -webkit-transform: rotate(-45deg);
    -ms-transform: rotate(-45deg);
    transform: rotate(-45deg);
  }

  .button-close:before {
    -webkit-transform: rotate(45deg);
    -ms-transform: rotate(45deg);
    transform: rotate(45deg);
  }
  .button-close:after,
  .button-close:before {
    content: "";
    position: absolute;
    height: 1px;
    width: 100%;
    top: 50%;
    left: 0;
    margin-top: -1px;
    background: gray;
  }

  .text-xl {
    font-size: 1.5rem;
  }
}
// .modal-body {
//   text-align: center;
// }
</style>
