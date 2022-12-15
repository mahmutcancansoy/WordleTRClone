<script setup>
import { reactive } from 'vue';

const props = defineProps({
  answer: {
    type: Array,
    required: true
  },
  line: {
    type: Number,
    required: true
  }
})

const payload = reactive({
  row: 6,
  column: 5
})
</script>

<template>
  <div 
  class="content"
  :style="{
    'grid-template-rows':`repeat(${payload.row},62px)`,
    'grid-template-column':`repeat(${payload.column},62px)`
  }"
  >
    <div 
    class="boxes" 
    v-for="(number,i) of payload.row * payload.column"
    :data-state="answer[i] ? answer[i].state :'empty'"
    >
    <template v-if="answer[i]">
      {{ answer[i].char.toUpperCase() }}
    </template>
  </div>
    
  </div>
</template>

<style scoped>
   .content {
     display: grid;
     align-items: center;
     justify-content: center;
     grid-template-rows: repeat(6,62px);
     grid-template-columns: repeat(5,62px);
     grid-gap: 10px;
     margin: 104px 0;

   }
   .boxes {
     width: 62px;
     height: 62px;
     display: flex;
     align-items: center;
     justify-content: center;
     background-color: #121213;
     border: 2px solid #3a3a3c;
     color: #d7dadc;
     font-size: 32px;
     line-height: 32px;
     font-weight: 700;
     user-select: none;
   }
   .boxes[data-state="active"] {
     border-color: #565758;
   }
   .boxes[data-state="wrong"] {
     border: none;
     background-color: #3a3a3c;
   }
   .boxes[data-state="wrong-location"] {
     border: none;
     background-color: #b59f3b;
   }
   .boxes[data-state="correct"] {
     border: none;
     background-color: #538d4e;
   }

</style>