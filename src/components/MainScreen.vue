<template>
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <div class="actions">
      <button @click="onStart(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>
      <button @click="onStart(36)">
        <span>6x6</span>
        <span>Normal</span>
      </button>
      <button @click="onStart(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button @click="onStart(100)">
        <span>10x10</span>
        <span>Super Hard</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onStart(totalOfBlock) {
      this.$emit("onStart", { totalOfBlock });
      this.$emit("getWidthMain");
    },
  },
};
</script>
<style scoped>
.screen {
  position: absolute;
  top: 30%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.screen h3,
h1,
.actions {
  text-align: center;
}
.screen h1 {
  font-size: 60px;
}
.screen h3 {
  margin-top: 10px;
  font-size: 30px;
}
.screen .actions {
  margin-top: 50px;
}

.screen .actions button {
  padding: 15px;
  margin-right: 20px;
  cursor: pointer;
  border: 1px solid white;
  border-radius: 10px;
}
.screen span {
  font-size: 16px;
  font-weight: bold;
  margin-right: 2px;
}
</style>
