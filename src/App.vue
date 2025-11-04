<script>
export default {
  data() {
    return {
      titles: {
        untilLessonStart: 'До начала урока',
        untilBreakFinish: 'До конца перерыва',
      },
      showingTitle: 'untilLessonStart'
    }
  },
  
  methods: {
    cycleTitles() {
      const titlesKeys = Object.keys(this.titles)
      const idx = titlesKeys.indexOf(this.showingTitle)
      let idxNext = idx + 1; if (idxNext === titlesKeys.length) idxNext = 0
      
      this.showingTitle = titlesKeys[idxNext]
    }
  }
}
</script>

<template>
  <main class="timer__wrap main cont">
    <p class="timer__wrap__title" @dblclick="cycleTitles" contenteditable>
      <slot>{{ titles[showingTitle] }}</slot>:
    </p>
    <section class="timer">

    </section>
    <p class="timer__wrap__subtitle" contenteditable>
      
    </p>
    <!-- Можно поиграть в Акинатор -->
  </main>
</template>
