<template>
  <div id="app">
      <h1>Monty Hall</h1>
      <Gift />
      <Error />
  </div>
</template>

<script>
import Gift from './components/Gift'
import Error from './components/Error'

export default {
  name: 'App',
  components: { Gift, Error }
}
</script>

<style>
*{
  box-sizing: border-box;
  font-family: 'Montserrat', sans-serif;
}

body {
  color: white;
  background: #121FCF;
  background: linear-gradient(to top right, #121FCF 0%, #ec06d9 89%);
}

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  height: 100vh;
}

#app h1 {
  text-shadow: 4px 2px 3px rgba(0, 0, 0, 0.68);
  background: #0008;
  padding: 20px;
  margin-bottom: 60px;
  border: 1px solid black;
}

</style>