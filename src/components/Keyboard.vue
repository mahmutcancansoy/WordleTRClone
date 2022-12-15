<script setup>
import { reactive, watch} from 'vue';

const props =defineProps({
  characters:Array
})
watch (() => props.characters,(characters) => {
  const list = [...payload.rows]
  for (const character of characters) {
    for (const row of list) {
      for (const letter of row) {
        if (letter.char.toUpperCase() === character.char.toUpperCase()){
          letter.state = character.state
        }
      }
    }
  }
  console.log({list, characters})
  payload.rows = list
})

const payload = reactive ({
  rows: [
    [
      { char: 'E', key: 'E', state: null },
      { char: 'R', key: 'R', state: null },
      { char: 'T', key: 'T', state: null },
      { char: 'Y', key: 'Y', state: null },
      { char: 'U', key: 'U', state: null },
      { char: 'I', key: 'I', state: null },
      { char: 'O', key: 'O', state: null },
      { char: 'P', key: 'P', state: null },
      { char: 'Ğ', key: 'Ğ', state: null },
      { char: 'Ü', key: 'Ü', state: null },
    ],
    [
      { char: 'A', key: 'A', state: null },
      { char: 'S', key: 'S', state: null },
      { char: 'D', key: 'D', state: null },
      { char: 'F', key: 'F', state: null },
      { char: 'G', key: 'G', state: null },
      { char: 'H', key: 'H', state: null },
      { char: 'J', key: 'J', state: null },
      { char: 'K', key: 'K', state: null },
      { char: 'L', key: 'L', state: null },
      { char: 'Ş', key: 'Ş', state: null },
      { char: 'İ', key: 'İ', state: null },
    ],
    [
      { char: 'ENTER', key: 'ENTER', state: null },
      { char: 'Z', key: 'Z', state: null },
      { char: 'C', key: 'C', state: null },
      { char: 'V', key: 'V', state: null },
      { char: 'B', key: 'B', state: null },
      { char: 'N', key: 'N', state: null },
      { char: 'M', key: 'M', state: null },
      { char: 'Ö', key: 'Ö', state: null },
      { char: 'Ç', key: 'Ç', state: null },
      { char: 'DELETE', key: 'DELETE', state: null },
    ]
  ]
})
</script>



<template>
  <div class="keyboard">
    <div class="row" v-for="(row, i) of payload.rows" :key="`row-${i}`">
      <div
        v-for="(letter, j) of row"
        class="letter"
        :class="letter.state"
        :data-key="letter.key"
      >
        {{ letter.char }}
      </div>
    </div>
  </div>
</template>


<style scoped>
    .keyboard {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    .row {
      width: 50%;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 8px;
    }
    .letter {
      height: 58px;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0 8px 0 0 ;
      border-radius: 4px;
      flex: 1;
      background-color: #818384;
      color: #d7dadc;
      font-weight: bold;
      cursor: pointer;
      user-select: none;
    }
    .spacer-half {
      flex: 0.5;
    }
    .icon-delete {
      font-size: 20px;
    }
    .letter.wrong {
      background-color: #3a3a3c;
    }
    .letter.wrong-location {
      background-color: #b59f3b;
    }
    .letter.correct {
      background-color: #538d4e;
    }

</style>