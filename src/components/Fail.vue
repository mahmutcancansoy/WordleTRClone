<script setup>
const emits = defineEmits(['close'])
const props = defineProps({
  correctAnswer: String
})
</script>
<template>
    <div class="popup">
        <div class="popup-bg" @click="emits('close')" />
        <div class="popup-content">
            Maalesef bulamadın!<br>Kelime: <b>{{ props.correctAnswer }}</b>
        </div>
    </div>
</template>

<style scoped>
.popup {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.popup-bg {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: 1;
  background-color: rgba(0,0,0,.5);
}

.popup-content {
  position: relative;
  z-index: 2;
  width: 540px;
  padding: 24px;
  border-radius: 8px;
  background-color: #ffffff;
  font-size: 24px;
  line-height: 36px;
  text-align: center;
}
</style>