<script setup lang="ts">
import { ref } from "vue";
import { onClickOutside } from "@vueuse/core";

const modal = ref(false);
const modalRef = ref(null);
const props = defineProps({
  triggerText: {
    default: "查看",
  },
  headText: {
    default: "服务端开发流程",
  },
  url: {
    default: "/server_development.png",
  },
});
const url = ref(props.url);
const headText = ref(props.headText);
const triggerText = ref(props.triggerText);
onClickOutside(modalRef, (event) => {
  modal.value = false;
});
</script>

<template>
  <button
    @click="modal = true"
    class="
      border-3 border-green-100
      p-2
      border-opacity-50
      text-light-50
      btn btn-green
    "
  >
    {{ triggerText }}
  </button>
  <transition name="fade">
    <div v-if="modal" ref="modalRef" class="modal border-2 bg-light-200">
      <div class="inner">
        <button
          class="button small btn btn-green"
          style="transform: scale(0.6)"
          title="Close"
          @click="modal = false"
        >
          𝖷
        </button>
        <p class="heading">{{ headText }}</p>
        <img
          :src="url"
          class="h-auto w-auto m-auto"
          :title="headText"
          :alt="headText"
        />
      </div>
    </div>
  </transition>
</template>

<style scoped>
.modal {
  position: fixed;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  height: auto;
  min-width: 39vw;
  max-width: 100%;
  z-index: 10;
}
.inner {
  background-color: var(--c-bg);
  padding: 4px;
  border-radius: 5px;
  border: 1px solid var(--c-divider-light);
  box-shadow: 2px 2px 10px rgba(10, 10, 10, 0.1);
}
.heading {
  font-weight: bold;
  font-size: 1rem;
  padding: 6px;
  margin: 0;
}
.button {
  position: absolute;
  top: 0;
  right: 0;
  font-weight: bold;
  color: white;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
.btn {
  border-radius: 0.5rem;
  font-weight: 600;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  padding-left: 1rem;
  padding-right: 1rem;
  --tw-shadow-color: 0, 0, 0;
  --tw-shadow: 0 4px 6px -1px rgba(var(--tw-shadow-color), 0.1),
    0 2px 4px -1px rgba(var(--tw-shadow-color), 0.06);
  -webkit-box-shadow: var(--tw-ring-offset-shadow, 0 0 #0000),
    var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow);
  box-shadow: var(--tw-ring-offset-shadow, 0 0 #0000),
    var(--tw-ring-shadow, 0 0 #0000), var(--tw-shadow);
}
.btn-green {
  --tw-bg-opacity: 1;
  background-color: rgba(16, 185, 129, var(--tw-bg-opacity));
  --tw-text-opacity: 1;
  color: rgba(255, 255, 255, var(--tw-text-opacity));
}
.btn-green:hover {
  --tw-bg-opacity: 1;
  background-color: rgba(4, 120, 87, var(--tw-bg-opacity));
}
*:focus {
  outline: none;
}
</style>
