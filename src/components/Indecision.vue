<template>
  <img :src="bgImage" alt="bg" v-if="bgImage">
  <div class="bg-dark"></div>

  <div class="indecision-container">
    <input type="text" placeholder="Hazme una pregunta" v-model="question">
    <p>Recuerda terminar con un signo de interrogación (?)</p>

    <div v-if="isValidQuestion">
      <h2>{{ question }}</h2>
      <h1>{{ answer }}</h1>
    </div>
  </div>
</template>

<script>
export default {
  name: "Indecision",
  data() {
    return {
      question: null,
      answer: null,
      bgImage: null,
      isValidQuestion: false,
    }
  },
  methods: {
    async getAnswer() {
      try {
        this.answer = 'Pensando...'
        const resp = await fetch('https://yesno.wtf/api');
        const { answer, image } = await resp.json();

        this.answer = answer;
        this.bgImage = image;
      } catch (e) {
        console.error(e);
      }
    }
  },
  watch: {
    question(value) {
      this.isValidQuestion = false;
      if (!value.includes('?')) return;

      this.getAnswer();
      this.isValidQuestion = true;
    }
  },
  computed: {
    answer: function () {
      return this.answer === 'yes' ? 'Si' : this.answer === 'maybe' ? 'Tal vez' : 'No';
    }
  }
}
</script>

<style scoped>

img, .bg-dark {
  height: 100vh;
  left: 0;
  max-height: 100%;
  max-width: 100%;
  position: fixed;
  top: 0;
  width: 100vw;
}

.bg-dark {
  background-color: rgba(0, 0, 0, 0.4);
}

.indecision-container {
  position: relative;
  z-index: 99;
}

input {
  width: 250px;
  padding: 10px 15px;
  border-radius: 5px;
  border: none;
}
input:focus {
  outline: none;
}

p {
  color: white;
  font-size: 20px;
  margin-top: 0;
}

h1, h2 {
  color: white;
}

h2 {
  margin-top: 150px;
}

</style>
