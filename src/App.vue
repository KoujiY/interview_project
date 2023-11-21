<script setup>
import { ref } from "vue";
import AppMainPage from "./components/AppMainPage.vue";

const modalState = ref(false);

function handleModalState() {
  modalState.value = !modalState.value;
}
</script>

<template>
  <AppMainPage :handle-modal-state="handleModalState"></AppMainPage>
</template>

<style>
body {
  margin: 0;
  padding: 0;
}
</style>
