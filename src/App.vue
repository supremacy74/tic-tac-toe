<template>
  <div class="wrapper">
    <div class="container">
      <Game />
    </div>
  </div>
</template>

<script>
import Game from '@/components/Game'

export default {
  name: 'App',
  components: {
    Game
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Heebo:wght@100;200;300;400;500;600;700;800;900&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  color: #0f0f0f;
}

html,
body {
  font-family: 'Heebo', sans-serif;
  font-size: 20px;
  font-weight: 300;
}

button {
  border: none;
  cursor: pointer;
}

.wrapper {
  background: radial-gradient(circle at 5%, #ff00f5, #ff005f);
  display: flex;
  justify-content: center;
  min-height: 100vh;
}

.container {
  width: min(100%, 540px);
  padding: 5%;
  display: flex;
  flex-direction: column;
  gap: .5rem;
}

.heading {
  text-align: center;
}
</style>
