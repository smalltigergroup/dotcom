<template>
  <section class="container">
    <div>
      <app-logo/>

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
       <a href="mailto:info@smalltigergroup.com?subject= How can Small Tiger help me in...">info@smalltigergroup.com</a>
      </p>
    </div>
  </section>
</template>

<script>
import AppLogo from "~/components/AppLogo.vue";

export default {
  components: {
    AppLogo
  },
  data() {
    return {
      words: [
        "business intelligence",
        "software strategy",
        "process optimization",
        "blockchain",
        "digital presence",
        "workplace strategy"
      ],
      wordIndex: 0,
      currentIndex: 0,
      currentWord: "",
      pauseTime: 300,
      inputInterval: 150,
      eraseInterval: 75,
      interval: null
    };
  },
  computed: {
    currentText() {
      return this.currentWord.substr(0, this.currentIndex);
    }
  },
  mounted() {
    this.initialize();
  },
  methods: {
    initialize() {
      this.wordIndex = 0;
      this.currentIndex = 0;
      this.setWord();
      this.tickForwards();
    },
    nextWord() {
      if (this.wordIndex >= this.words.length - 1) {
        this.initialize();
      } else {
        this.wordIndex = this.wordIndex + 1;
        this.currentIndex = 0;
        this.setWord();
        this.tickForwards();
      }
    },
    setWord(){
        this.currentWord = this.words[this.wordIndex];
    },
    tickForwards() {
      this.interval = setInterval(() => {
        this.currentIndex = this.currentIndex + 1;
      }, this.inputInterval);
    },
    tickBackwards() {
      this.interval = setInterval(() => {
        this.currentIndex = this.currentIndex - 1;
      }, this.eraseInterval);
    }
  },
  watch: {
    currentIndex: {
      handler() {
        if (
          this.currentIndex - this.pauseTime / 100 >=
          (this.currentWord.length + 1)
        ) {
          //start ticking backwards after a slight weight time
          clearInterval(this.interval);
          this.tickBackwards();
        } else if (this.currentIndex < 0) {
          clearInterval(this.interval);
          this.nextWord();
        }
      }
    }
  }
};
</script>

<style>

@keyframes fade {
  to {
    background-color: black
   }
}

.container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  background-color: #000b4d;
  animation: fade 5s linear alternate infinite;
}

.subtext {
  font-family: "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif; /* 1 */
  display: block;
  font-weight: 300;
  font-size: 1em;
  color: #ffffff;
  letter-spacing: 1px;
  padding-top: 20px;
  padding-bottom: 20px;
}

.subtext a {
  display: block;
  color: #ffffff;
}

.subtitle {
  height: 1.5em;
  font-weight: 300;
  font-size: 2em;
  color: #ffffff;
  word-spacing: 5px;
  padding-bottom: 15px;
}

</style>
