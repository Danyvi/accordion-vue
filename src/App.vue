<template>
  <div id="app">
    <header>
      <h1>VUE<span>CORDION</span></h1>
    </header>
    <div class="faq">
      <Faq 
        v-for = "(faq,i) in faqs" 
        :key = "i" 
        :faq = "faq"
        :index = "i"
        :open = "faq.open"
        @toggleOpen="toggleOpen"
      />
    </div>
  </div>
</template>

<script>
import Faq from './components/Faq'

export default {
  name: 'App',
  components: {
    Faq
  },
  data() {
    return {
      faqs: [
        {
          question: "who is the best superhero?",
          answer: "I'm not sure but we love him 3000",
          open: false
        },
        {
          question: "What is Goku's form called ith White Hair?",
          answer: "Mastered Ultra Instinct",
          open: false
        },
        {
          question: "Have you eaten?",
          answer: "yes",
          open: false
        }
      ]
    }
  },
  methods: {
    toggleOpen(index) {
      this.faqs = this.faqs.map( (faq, i) => {
        if (index === i) {
          faq.open = !faq.open;
        } else {
          // this prevents that you can open multiple items at the same time
          faq.open = false;
        }

        return faq;
      });
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #eee;
  font-family: sans-serif;
}

header {
  background-color: #3c3c3c;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
}

header h1 {
  color: #eee;
  font-size: 28px;
  font-weight: 300;
  text-transform: uppercase;
}

header h1 span {
  color: #56e3b8;
  font-weight: 900;
}

.faq {
  display: block;
  width: 100%;
  max-width: 768px;
  margin: 15px auto;
  padding: 15px;
  background-color: #FFF;
  border-radius: 8px;
  box-shadow: 0px 0px 10px rgba(0,0,0,0.2);
}

.faq .question{
  position: relative;
  color: #3c3c3c;
  font-size: 20px;
  transition: all 0.4s linear;

  /* border: 1px solid red; */
}

.faq .question::after {
  /* border: 1px solid blue; */
  content: '';
  position: absolute;
  top: 50%;
  right: 0px;
  transform: translateY(-50%) rotate(0deg);

  height: 30px;
  width: 30px;
  background-image: url('./assets/arrow-down-mint.svg');
  background-position: center;
  background-size: contain;
  background-repeat: no-repeat;

  transition: all 0.2s linear;
}

.faq .open .question {
  margin-bottom: 15px;
}

.faq .open .question::after {
  transform: translateY(-50%) rotate(90deg);
}

.faq .answer {
  /* border: 1px solid magenta; */
  color: #3c3c3c;
  font-size: 18px;
  opacity: 1;
  max-height: 0px;
  overflow: hidden; 
  transition: all 0.4s ease-out;
}

.faq .open .answer {
  opacity: 1;
  max-height: 1000px;
}

</style>
