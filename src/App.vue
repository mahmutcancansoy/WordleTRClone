<script setup>
import Header from './components/Header.vue'
import Content from './components/Content.vue'
import Keyboard from './components/Keyboard.vue'
import Succcess from './components/Success.vue'
import Fail from './components/Fail.vue'
import { reactive } from 'vue'

const payload = reactive({
  nuberOfTries: 0,
  result: false,
  correctAnswer: 'SELAM',
  word: '',
  line: 0,
  answer: [],
  characters: []
})

const getState = (correctAnswer, char, index) => {
  if (correctAnswer.toUpperCase().includes(char.toUpperCase())) {
    if (correctAnswer[index] === char.toUpperCase()) {

      return 'correct'
    } else {
      return 'wrong-location'
    }
  }
  return 'wrong'
}

const check = () => {
  if (payload.word) {
    const answer = []
    for (let i = 0; i < 5; i++) {
      const data = {
        char: payload.word[i],
        state: getState(payload.correctAnswer, payload.word[i], i)
      }
      answer.push(data)
    }
    payload.line++
    payload.answer.push(...answer)
  }
}

const getWord = (event) => {
  if (payload.word.length > 0 && (event.key === 'Backspace' || event.key === 'Delete')) {
    payload.word = payload.word.substring(0, payload.word.length - 1)
    payload.answer.pop()
  }
  else if (event.key === 'Enter') {
    if (payload.word.length !== 5) {
      console.log('5 karakterli bir kelime girmelisin')
    }

    payload.answer.splice(payload.answer.length - 5, 5)
    check()
    payload.word = ''
    payload.characters = [...payload.answer]

    checkResult()
  }
  else if (event.key.length === 1) {
    if (payload.word.length === 5) {
      console.log('Maksimum 5 karakter girebilirsin')
      return false
    }

    payload.word += event.key

    const data = {
      char: event.key,
      state: 'empty'
    }

    payload.answer.push(data)
  }
}

const checkResult = () => {
  const last5Elements = payload.answer.slice(-5)
  payload.result = last5Elements.every(item => item.state === 'correct')
  payload.numberOfTries = payload.answer.length / 5 

}


</script>

<template>
  <div id="app" @keyup="getWord" tabindex="1">
    <congratulations />
    <Header />
    <Succcess 
      v-if="payload.result"
      @close="payload.popup = false"
      :numberOfTries="payload.numberOfTries"
    />
    <Fail
      v-else-if="payload.numberOfTries > 5"
      @close ="payload.popup = false"
      :correctAnswer="payload.correctAnswer"
    />
    <Content
      :line="payload.line"
      :answer="payload.answer"
    />
    <Keyboard 
      :characters="payload.characters"
    />
  </div>

</template>

<style scoped>
    #app {
      width: 100vw;
      height: 100vh;
      background-color: #121213;
      font-family: 'Roboto',sans-serif;
    }
</style>
