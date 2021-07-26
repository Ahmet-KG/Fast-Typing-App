<template>
  <div class="container jumbotron">
    <h1 class="display-4">Speed Writing Competition</h1>
    <p class="lead">Improve your Typing Speed</p>
    <hr class="my-4" />
    <div v-if="isFinish" class="alert alert-primary">
      <h1>Game Over</h1>
    </div>
    <div v-else>
    <div class="card">
      <div class="card-body">
        <span
          v-for="(word, key) in words.filter((data, index) => index < 20)"
          :key="key"
          :class="key != 0 || wordControl"
          class="ms-2 fs-3"
          >{{ word }}</span
        >
      </div>
    </div>
    <div class="card">
      <div class="card-body bg-secondary">
        <div class="input-group input-group-lg">
          <input type="text" class="form-control" v-model="writingWord" />
          <button class="btn btn-light" disabled type="button">
            {{timer}} sec
          </button>
          <button :disabled='isRunning' class="btn btn-light" type="button" @click="getWords">
            Refresh
          </button>
        </div>
      </div>
    </div>
    </div>
  </div>
</template>

<script>
import wordList from '@/assets/wordlist.json'
export default {
  data () {
    return {
      words: [],
      writingWord: null,
      isTrue: true,
      trueCount: 0,
      falseCount: 0,
      timer: 60,
      interval: false,
      isRunning: false,
      isFinish: false,
      wordList: wordList
    }
  },
  watch: {
    writingWord (val) {
      if (!val || val === ' ') {
        this.writingWord = ''
        return
      }
      if (!this.isRunning) this.toggleTimer()
      const word = this.words[0].slice(0, val.length)
      const usersWord = val.trim()
      this.isTrue = word === usersWord
      if (val.indexOf(' ') !== -1) {
        this.isTrue ? this.trueCount++ : this.falseCount++
        this.words.splice(0, 1)
        this.writingWord = ''
        this.isTrue = true
      }
    }
  },
  computed: {
    wordControl () {
      return this.isTrue ? 'focused-word' : 'focused-word bg-danger'
    }
  },

  mounted () {
    this.getWords()
  },

  methods: {
    getWords () {
      this.words = this.wordList.sort(() => Math.random() - 0.5).splice(0, 300)
    },
    toggleTimer () {
      this.isRunning = true
      this.interval = setInterval(this.timeProcess, 1000)
    },
    timeProcess () {
      if (this.timer === 0) {
        clearInterval(this.interval)
        this.isFinish = true
        return
      }
      this.timer--
    }
  }
}
</script>

<style>
.jumbotron {
  padding: 3rem 2rem;
  margin-bottom: 2rem;
  background-color: #e9ecef;
  border-radius: 0.3rem;
}
.focused-word {
  background-color: slategray;
  color: #fff;
  padding: 5px;
  border-radius: 4px;
}
</style>
