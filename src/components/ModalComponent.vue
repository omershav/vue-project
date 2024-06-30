<script setup>
import { defineProps, defineEmits, ref } from "vue";
import { onClickOutside } from "@vueuse/core";

const props = defineProps({
  isOpen: Boolean,
  imageUrl: String,
  modalHeader: String,
  buttonText: String,
  buttonUrl: String,
});

const emit = defineEmits(["modal-close"]);

const target = ref(null);
onClickOutside(target, () => emit("modal-close"));
</script>

<template>
  <div v-if="isOpen" class="modal-mask">
    <div class="modal-container" ref="target">
      <div class="modal-close">
        <span @click.stop="emit('modal-close')">X</span>
      </div>
      <div class="modal-wrapper">
        <div class="modal-image"><img :src="imageUrl" /></div>
        <div class="modal-header">{{ modalHeader }}</div>
        <div class="modal-btn">
          <a :href="buttonUrl">
            <button>{{ buttonText }}</button>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal-image {
  margin-bottom: 20px;
}

.modal-btn button {
  background-color: #80c144;
  border: none;
  color: white;
  width: 217px;
  height: 38px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  cursor: pointer;
  font-weight: 600;
  font-size: 16px;
  line-height: 24px;
  margin: 25px 0px;
  border-radius: 6px;
}

.modal-btn button:hover {
  background-color: #76b041;
}

.modal-container {
  background-color: #f9f8f2;
}

.modal-close {
  text-align: right;
}

.modal-close span {
  cursor: pointer;
  color: #162a45;
}

.modal-close a:hover {
  color: #1b3352be;
}

.modal-wrapper {
  text-align: center;
}

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.2);
}

.modal-header {
  color: #2b8a19;
  font-weight: 500;
  font-size: 26px;
  margin: 10px;
  line-height: 24px;
}

.modal-container {
  width: 276px;
  height: 321px;
  margin: 150px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 6px;
  border: 2px solid #7cd16e;
}
</style>