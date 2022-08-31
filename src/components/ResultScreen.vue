<template>
  <div class="screen">
    <h1>End game</h1>
    <p>Time game: {{ timeEndGame }}</p>
    <button @click="$emit('onReStart')">Restart</button>
  </div>
</template>
<script>
export default {
  props: {
    timeEndGame: {
      type: String,
      required: true,
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
  text-align: center;
}
.screen h3,
h1,
p {
  text-align: center;
}
.screen h1 {
  font-size: 60px;
}
.screen p {
  margin-top: 10px;
  font-size: 30px;
}
.screen button {
  margin-top: 30px;
  padding: 10px 15px;
  border: 1px solid white;
  border-radius: 5px;
  font-size: 20px;
  font-weight: bold;
  cursor: pointer;
}
</style>
