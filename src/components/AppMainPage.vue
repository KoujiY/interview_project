<script setup>
const props = defineProps({ handleModalState: Function });
const ballListArray = [0, 2, 6, 8];

function judgeFlash(index) {
  if (index === 2 || index === 4 || index === 8) {
    return true;
  } else {
    return false;
  }
}
</script>

<template>
  <div class="header-line">
    <button @click="props.handleModalState()">menu</button>
  </div>
  <div class="outer-box">
    <div class="box-wrapper">
      <div
        class="inner-box"
        v-for="(box, index) in 9"
        :key="`box${box}`"
        :class="{ 'inner-box--flash': judgeFlash(index) }"
      ></div>
      <div
        class="inner-ball"
        v-for="ball in ballListArray"
        :key="`ball${ball}`"
        :style="`--position-x: ${ball % 3}; --position-y: ${Math.floor(
          ball / 3
        )};`"
      ></div>
    </div>
  </div>
</template>

<style scoped>
.header-line {
  width: 100%;
  height: 40px;
  padding: 4px;
  box-sizing: border-box;
  display: flex;
  flex-direction: row-reverse;
}

.outer-box {
  width: 100%;
  height: calc(100vh - 40px);
  background-color: gainsboro;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

.box-wrapper {
  width: fit-content;
  display: grid;
  grid-template-columns: repeat(3, auto);
  grid-template-rows: repeat(3, auto);
  gap: 8px;
  position: relative;
}

.inner-box {
  width: 30vw;
  height: 100px;
  border: black solid 2px;
  background: radial-gradient(
    circle,
    rgba(113, 81, 95, 1) 81%,
    rgba(0, 0, 0, 1) 100%
  );
  box-sizing: border-box;
}

.inner-box--flash {
  animation: flash 0.5s ease-in-out 0s infinite;
}

@keyframes flash {
  0% {
    opacity: 60%;
  }

  100% {
    opacity: 100%;
  }
}

.inner-ball {
  width: 30px;
  height: 30px;
  background-color: #a5f12b;
  border-radius: 50%;
  position: absolute;
  top: calc(var(--position-y, 0) * (100px + 8px) + 50px - 15px);
  left: calc(var(--position-x, 0) * (30vw + 8px) + 15vw - 15px);
  animation: move 1.5s ease-out 0s infinite;
}

@keyframes move {
  0% {
    transform: translateX(0);
  }

  100% {
    transform: translateX(calc(2 * (30vw + 8px)));
  }
}
</style>
