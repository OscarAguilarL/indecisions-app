<template>
  <h2>{{ customTitle }}</h2>
  <p>{{ count }} <sup>2</sup> = {{ getSquare }}</p>

  <button @click="incrementCount">+1</button>
  <button @click="decrementCount">-1</button>
</template>

<script>
export default {
  name: "Counter",
  props: {
    title: String,
    start: {
      type: Number,
      default: 1,
    },
  },
  data() {
    return {
      count: this.start || 0,
    };
  },
  methods: {
    incrementCount() {
      this.count++;
    },
    decrementCount() {
      this.count--;
    },
  },
  computed: {
    getSquare() {
      return this.count * this.count;
    },
    customTitle() {
      return this.title || "Counter";
    },
  },
};
</script>

<style scoped>
button {
  background-color: #64b687;
  border-radius: 5px;
  border: 1px solid white;
  color: white;
  cursor: pointer;
  margin: 0 5px;
  padding: 5px 15px;
  transition: 0.3s ease-in-out;
}

button:hover {
  background-color: #5aa67b;
}
</style>
