<template>
  <transition name="fade">
    <div v-if="open" class="modal-base">
      <transition name="drop">
        <div class="inner col-6 mt-5 mx-auto" v-show="open">
          <div class="content bg-white rounded px-4 pt-5 pb-4">
            <slot />
            <button
              class="close btn btn-secondary fs-6 py-0 px-1"
              @click="close"
            >
              <i class="bi bi-x"></i>
            </button>
          </div>
        </div>
      </transition>
    </div>
  </transition>
</template>

<script setup>
import { defineProps, defineEmits, onMounted, onUnmounted } from "vue";

const props = defineProps({
  open: {
    type: Boolean,
    required: true,
  },
});

const emit = defineEmits(["close"]);

function close() {
  emit("close");
}

function handleKeyup(event) {
  if (event.keyCode === 27) {
    close();
  }
}

onMounted(() => document.addEventListener("keyup", handleKeyup));
onUnmounted(() => document.removeEventListener("keyup", handleKeyup));

console.log(props);
</script>

<style scoped>
.modal-base {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow-x: hidden;
  overflow-y: auto;
  background-color: rgba(0, 0, 0, 0.4);
  z-index: 1;
}

.content {
  position: relative;
}

.close {
  position: absolute;
  top: 10px;
  right: 15px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.drop-enter-active,
.drop-leave-active {
  transition: all 0.5s ease-in-out;
}

.drop-in-enter-from,
.drop-in-leave-to {
  opacity: 0;
  transform: translateY(-50px);
}
</style>
