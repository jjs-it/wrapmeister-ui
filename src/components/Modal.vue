<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div
        class="modal"
        role="dialog"
        aria-labelledby="modalTitle"
        aria-describedby="modalDescription"
      >
        <header class="modal-header" id="modalTitle">
          <slot name="header"> </slot>
        </header>

        <section class="modal-body" id="modalDescription">
          <slot name="body">
            {{ body }}
          </slot>
        </section>

        <footer class="modal-footer">
          <slot name="footer"> </slot>

          <div class="modcontainer">
            <div class="moditem">
              <m-button
                class="m-top-sm margin-auto"
                type="success"
                @mbclick="confirm"
                >Confirm</m-button
              >
            </div>
            <div class="moditem">
              <m-button
                class="m-top-sm margin-auto"
                type="danger"
                @mbclick="close"
                >Cancel</m-button
              >
            </div>
          </div>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
import MButton from "@/components/Button.vue";

export default {
  name: "Modal",
  props: {
    body: {
      type: String,
      default: "Proceed with MetaMask?",
    },
  },

  methods: {
    close() {
      this.$emit("modalclose");
    },
    confirm() {
      this.$emit("modalconfirm");
    },
  },
  components: {
    MButton,
  },
};
</script>

<style lang="scss" scoped>
.modal-backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.3);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}

.modal {
  background: #ffffff;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
}

.modal-header,
.modal-footer {
  padding: 15px;
  display: flex;
}

.modal-header {
  position: relative;
  border-bottom: 1px solid #eeeeee;
  color: #4aae9b;
  justify-content: space-between;
}

.modal-footer {
  border-top: 1px solid #eeeeee;
  flex-direction: column;
}

.modal-body {
  position: relative;
  padding: 20px 10px;
}

.btn-close {
  position: absolute;
  top: 0;
  right: 0;
  border: none;
  font-size: 20px;
  padding: 10px;
  cursor: pointer;
  font-weight: bold;
  color: #4aae9b;
  background: transparent;
}

.modcontainer {
  display: flex;
}

.moditem { 
  flex-basis: 100px;
  height: 50px;
  margin: 5px;
}

.btn-green {
  color: white;
  background: #4aae9b;
  border: 1px solid #4aae9b;
  border-radius: 2px;
}

.modal-fade-enter,
.modal-fade-leave-to {
  opacity: 0;
}

.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.5s ease;
}
</style>
