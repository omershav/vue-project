<script setup>
import { ref, onMounted } from "vue";
import ModalComponent from "../components/ModalComponent.vue";

const isModalOpened = ref(false);
const modals = ref(null);

const openModal = () => {
  isModalOpened.value = true;
};
const closeModal = () => {
  isModalOpened.value = false;
};

onMounted(async () => {
  try {
    const response = await fetch("https://app-api.wzc.mk/");
    const data = await response.json();
    modals.value = data;
  } catch (error) {
    console.error("Error fetching JSON:", error);
  }
});
</script>

<template>
  <div>
    <button @click="openModal" class="open-modal">Open modal</button>
  </div>
  <ModalComponent
    v-if="modals"
    :isOpen="isModalOpened"
    @modal-close="closeModal"
    @submit="submitHandler"
    :imageUrl="modals[0].image_url"
    :modalHeader="modals[0].text"
    :buttonText="modals[0].btn_text"
    :buttonUrl="modals[0].btn_url"
  >
  </ModalComponent>
</template>

<style scoped>
.open-modal {
  background-color: #80c144;
  border: none;
  color: white;
  padding: 8px 40px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  cursor: pointer;
  font-weight: 600;
  font-size: 16px;
  line-height: 24px;
  margin: 20px 0px;
  border-radius: 6px;
}
</style>