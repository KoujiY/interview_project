<script setup>
import { ref } from "vue";
import AppMainPage from "./components/AppMainPage.vue";
import AppSideMenu from "./components/AppSideMenu.vue";

const modalState = ref(false);

function handleModalState() {
  modalState.value = !modalState.value;
}
</script>

<template>
  <section>
    <AppMainPage :handle-modal-state="handleModalState"></AppMainPage>
    <AppSideMenu
      :modal-state="modalState"
      :handle-modal-state="handleModalState"
    ></AppSideMenu>
  </section>
</template>

<style>
body {
  margin: 0;
  padding: 0;
}
</style>
