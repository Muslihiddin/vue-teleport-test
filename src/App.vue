<script setup>
import { ref } from "vue";
import { onClickOutside } from "@vueuse/core";

const isModalOpen = ref(false);
const modal = ref(null);
onClickOutside(modal, () => (isModalOpen.value = false));
</script>

<template>
  <div>
    <h1>Teleport modal</h1>
    <button @click="isModalOpen = true">Open modal</button>
    <Teleport to="#modal">
      <Transition name="modal">
        <div class="modal-bg" v-if="isModalOpen">
          <div ref="modal" class="modal">
            <p>To close modal press button or click outside of modal</p>
            <button @click="isModalOpen = false">Close modal</button>
          </div>
        </div>
      </Transition>
    </Teleport>
  </div>
</template>

<style scoped>
.modal-bg {
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.5);
}

.modal {
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 10px;
  background-color: rgb(80, 80, 80);
  width: 450px;
  height: 120px;
  color: rgb(209, 209, 209);
}

.modal-enter-active,
.modal-leave-active {
  transition: all 0.25s ease;
}
.modal-enter-from,
.modal-leave-to {
  opacity: 0;
  transform: scale(1.1);
}
</style>
