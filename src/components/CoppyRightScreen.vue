<template>
  <div class="copy__right">
    <p>
      This game owned by RHP Team in Vue 3 course for begginers -
      <a href="#">view here</a>
    </p>
  </div>
</template>

<style lang="css">
.copy__right {
  position: fixed;
  color: var(--light);
  z-index: 3;
  font-size: 25px;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  padding: 15px 0;
}

.copy__right a {
  color: darkgoldenrod;
}
</style>
