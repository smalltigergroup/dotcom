<template>
  <section class="container">
    <div>
      <app-logo/>

      <p class='subtext'>
        small tiger
      </p>

      <h2 class="subtitle">
        {{currentText}}
      </h2>

      <p class='subtext'>
        businesses world wide rely on 
        <br>
        the expertise of small tiger group
        <br>
        to put ideas into production
      </p>


      <p class='subtext'>
        contact us
       <a href="mailto:info@smalltigergroup.com">info@smalltigergroup.com</a>
      </p>
    </div>
  </section>
</template>

<script>

import AppLogo from '~/components/AppLogo.vue'

export default {
  components: {
    AppLogo,
  },
  data() {
    return {
      words: [
        'design',
        'digital presence',
        'business intelligence',
        'workplace strategy'
      ],
      wordIndex: 0,
      currentIndex: 0,
      currentWord: '',
      pauseTime: 400,
      inputInterval: 200,
      eraseInterval: 150,
      interval: null,
    }
  },
  computed: {
    currentText(){
      return this.currentWord.substr(0, this.currentIndex);
    }
  },
  mounted(){
    this.initialize();
  },
  methods: {
    initialize(){
      this.wordIndex = 0;
      this.currentWord = this.words[this.wordIndex];
      this.tickForwards();
    },
    nextWord(){
      if(this.wordIndex >= this.words.length - 1) {
        console.log('back to beginning')
        this.wordIndex = 0;
        this.currentIndex = 0;
        this.currentWord = this.words[this.wordIndex];
        this.tickForwards()
      } else {
        console.log('next!')
        this.wordIndex = this.wordIndex + 1
        this.currentIndex = 0;
        this.currentWord = this.words[this.wordIndex];
        this.tickForwards()
      }
    },
    tickForwards(){
      this.interval = setInterval(()=>{
        this.currentIndex = this.currentIndex + 1
      }, this.inputInterval)
    },
    tickBackwards(){
      this.interval = setInterval(()=>{
        this.currentIndex = this.currentIndex - 1
      }, this.eraseInterval)
    }
  },
  watch: {
    currentIndex:{
      handler(){
        if(this.currentIndex - (this.pauseTime/100) >= this.currentWord.length + 1){
          clearInterval(this.interval);
          this.tickBackwards()
        } else if (this.currentIndex < 0){
          clearInterval(this.interval);
          this.nextWord();
        }
      }
    }
  }
}
</script>

<style>

.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  background-color: black;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.vue-typer {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtext{
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 1em;
  color: #ffffff;
  letter-spacing: 1px;
  padding-top: 20px;
  padding-bottom: 20px;
}

.subtext a{
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 1em;
  color: #ffffff;
  letter-spacing: 1px;
  padding-bottom: 20px;
}

.subtitle {
  height: 1.5em;
  font-weight: 300;
  font-size: 2em;
  color: #ffffff;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

button {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  background-color: #000000;
  border-color: #dbdbdb;
  border-width: 1px;
  color: #ffffff;
  justify-content: center;
  padding-bottom: calc(1.375em - 1px);
  padding-left: .75em;
  padding-right: .75em;
  padding-top: calc(1.375em - 1px);
  text-align: center;
  white-space: nowrap;
  border-radius: .5em;
}
</style>
