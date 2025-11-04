<script>
export default {
  data() {
    return {
      titles: {
        untilLessonStart: 'До начала урока',
        untilTypingFinish: 'До конца печатания',
        untilBreakFinish: 'До конца перерыва',
        untilIndependentWorkFinish: 'Самостоятельная работа. До её конца',
        untilLessonFinish: 'До конца урока',
      },
      showingTitle: 'untilLessonStart',
      minutesText: null,
      secondsText: null,
      seconds: 0,
      futureHours: null,
      futureMinutes: null,
    }
  },
  
  methods: {
    cycleTitles() {
      const titlesKeys = Object.keys(this.titles)
      const idx = titlesKeys.indexOf(this.showingTitle)
      let idxNext = idx + 1; if (idxNext === titlesKeys.length) idxNext = 0
      
      this.showingTitle = titlesKeys[idxNext]
    },
    startCountdown() {
      document.activeElement.blur()

      console.log(this.minutesText, this.secondsText)

      const secondsSummed = Number(this.minutesText) * 60 + Number(this.secondsText)
      this.seconds = secondsSummed
      console.log(this.seconds)
      const interval = setInterval(() => {
        this.seconds--

        console.log(this.seconds)

        if (this.seconds % 60 < 10) this.secondsText = '0' + this.seconds % 60
        else this.secondsText = this.seconds % 60

        const minutesRes = Math.trunc(this.seconds / 60)
        if (minutesRes < 10) this.minutesText = '0' + minutesRes
        else this.minutesText = minutesRes

        if (this.seconds === 0) clearInterval(interval)
      }, 1000)

      const now = new Date()
      const futureTime = new Date(now.getTime() + secondsSummed * 1000)
      this.futureHours = futureTime.getHours()
      this.futureMinutes = futureTime.getMinutes()
      console.log(this.futureHours, this.futureMinutes)
    }
  }
}
</script>

<template>
  <main class="timer__wrap main cont">
    <p class="timer__wrap__title" @dblclick="cycleTitles" contenteditable>
      {{ titles[showingTitle] }}:
    </p>
    <section class="timer" @keyup.enter="startCountdown">
      <input v-model="minutesText" class="timer__input timer__input__minutes" placeholder="00">:<input v-model="secondsText" class="timer__input timer__input__seconds" placeholder="00">
    </section>
    <p v-if="this.futureHours" class="timer__wrap__time-after-countdown">
      <span class="timer__wrap__time-after-countdown__text">{{ futureHours }} : {{ futureMinutes }}</span>
    </p>
    <p class="timer__wrap__subtitle" contenteditable>
      
    </p>
    <!-- Можно поиграть в Акинатор -->
  </main>
</template>
