<template lang="">
  <div class="screen">
    <h1>POKE MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <div class="action">
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
        <span>Super hard</span>
      </button>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    onStart(totalOfBlocks) {
      this.$emit("onStart", { totalOfBlocks: totalOfBlocks });
    },
  },
};
</script>

<style>
.screen {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  background-color: var(--dark);
  color: var(--light);
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: center;
}

.screen h1 {
  font-size: 50px;
}
.action {
  padding: 15px 0;
}
.action button {
  padding: 30px 20px;
  width: 150px;
  border-radius: 10px;
  margin: 0 5px;
  cursor: pointer;
  transition: ease-in-out 0.2s;
}
.action button:hover {
  background-color: rgb(228, 107, 26);
  transform: scale(110%);
}
</style>
