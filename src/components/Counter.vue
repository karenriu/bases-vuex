<template>
  <h1>Counter - Vue</h1>
  <h2>Direct access: {{ $store.state.counter.count }}</h2>
  <h2>Computed: {{ countComputed }}</h2>
  <div>
    <button @click="increment">+1</button>
    <button @click="incrementBy">+5</button>
    <button @click="incrementRandomInt" :disabled="isLoading">Random</button>
  </div>

  <h1>mapState</h1>
  <h2>mapState: {{ count }}</h2>
  <h2>lastMutation: {{ lastMutation }}</h2>

  <h2>Direct Getter: {{ $store.getters["counter/squareCount"] }}</h2>
</template>

<script>
import { mapState, mapActions } from "vuex";

export default {
  //computed: mapState(["count"]),

  computed: {
    countComputed() {
      return this.$store.state.counter.count;
    },
    ...mapState("counter", ["count", "lastMutation", "isLoading"]),
    // ...mapState({
    //   count: (state) => state.count,
    //   lastMutation: (state) => state.lastMutation,
    // }),
  },

  methods: {
    increment() {
      this.$store.commit("counter/increment");
    },
    incrementBy() {
      this.$store.commit("counter/incrementBy", 5);
    },
    ...mapActions("counter", ["incrementRandomInt"]),
    // ...mapActions({
    //   randomInt: "incrementRandomInt",
    // }),
  },
};
</script>
