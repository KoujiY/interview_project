<script setup>
import { reactive, watch } from "vue";
import MenuItem from "./MenuItem.vue";
import data from "../assets/data.json";

const props = defineProps({ modalState: Boolean, handleModalState: Function });
const menuOpenArray = reactive([]);
const openFlagArray = reactive(data.map(() => false));

function handleOpenArray(level, count) {
  if (menuOpenArray[level] !== undefined) {
    for (let i = 0; i < menuOpenArray.length; i++) {
      if (i > level) {
        menuOpenArray[i] = -1;
      }
      if (i === level) {
        if (menuOpenArray[i] === count) {
          menuOpenArray[i] = -1;
        } else {
          menuOpenArray[i] = count;
        }
      }
    }
  } else {
    menuOpenArray[level] = count;
  }
}

watch(menuOpenArray, (nV) => {
  openFlagArray.forEach((el, index) => {
    nV[0] === index
      ? (openFlagArray[index] = true)
      : (openFlagArray[index] = false);
  });
});
</script>

<template>
  <div
    class="modal-wrapper"
    @click.stop="props.handleModalState"
    :class="{ 'modal-wrapper--opened': props.modalState }"
  >
    <div class="inner-menu" @click.stop="() => {}">
      <MenuItem
        v-for="(menuData, index) in data"
        :menu-data="menuData"
        :key="menuData.key"
        :level="0"
        :count="index"
        :open-array="menuOpenArray"
        :handle-open-array="handleOpenArray"
        :open-flag="openFlagArray[index]"
      ></MenuItem>
      <!-- 末端會誤觸發最後一個menu選項，暫時沒有頭緒，先放一個li擋著 -->
      <li style="height: 100px" @click.stop="() => {}"></li>
    </div>
  </div>
</template>

<style scoped>
.modal-wrapper {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 100%;
  transition: left 0.4s ease;
}

.inner-menu {
  width: 50%;
  height: 100vh;
  margin: 0 0 0 auto;
  padding: 0;
  background-color: rgb(0, 0, 0, 0.95);
  box-sizing: border-box;
}

.modal-wrapper--opened {
  left: 0;
}
</style>
