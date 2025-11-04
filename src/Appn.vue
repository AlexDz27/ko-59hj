<script setup>
import { ref } from 'vue'

const titles = {
  untilLessonStart: 'До начала урока',
  untilTypingFinish: 'До конца печатания',
  untilBreakFinish: 'До конца перерыва',
  untilIndependentWorkFinish: 'Самостоятельная работа. До её конца',
  untilLessonFinish: 'До конца урока',
}
const currentTitleKey = ref('untilTypingFinish')
function cycleTitles() {
  const titlesKeys = Object.keys(titles)
  const idx = titlesKeys.indexOf(currentTitleKey.value)
  let idxNext = idx + 1; if (idxNext === titlesKeys.length) idxNext = 0

  currentTitleKey.value = titlesKeys[idxNext]
}
</script>

<template>
  <main class="timer__wrap main cont">
    <p class="timer__wrap__title" @keyup.enter="cycleTitles" contenteditable>
      {{ titles[currentTitleKey] }}:
    </p>
    <section class="timer" @keyup.enter="startCountdown">
      <input v-model="minutesText" class="timer__input timer__input__minutes" placeholder="00">:<input v-model="secondsText" class="timer__input timer__input__seconds" placeholder="00">
    </section>
    <p class="timer__wrap__subtitle" contenteditable>
      
    </p>
    <!-- Можно поиграть в Акинатор -->
  </main>
</template>