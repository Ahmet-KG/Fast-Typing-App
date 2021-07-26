<template>
  <div class="container jumbotron">
    <h1 class="display-4">Speed Writing Competition</h1>
    <p class="lead">Improve your Typing Speed</p>
    <hr class="my-4" />

    <div class="card">
      <div class="card-body">
        <span
          v-for="(word, key) in words"
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
            1:00
          </button>
          <button class="btn btn-light" type="button">
            Refresh
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      words: [
        'ucak',
        'lale',
        'bilgisayar',
        'kalem',
        'araba',
        'okumak',
        'telefon',
        'almanya'
      ],
      writingWord: null,
      isTrue: true
    }
  },
  watch: {
    writingWord (val) {
      const word = this.words[0].slice(0, val.length)
      if (word === val) {
        console.log('dogru')
      } else {
        this.isTrue = false
      }
    }
  },
  computed: {
    wordControl () {
      return this.isTrue ? 'focused-word' : 'focused-word bg-danger'
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
