<template>
  <div class="error">
      <img src="../assets/imgs/error.gif">
  </div>
</template>

<script>
export default {
 name: 'Error'
}
</script>

<style>
 .error {
     position: relative;
     display: flex;
     align-items: center;
     justify-content: center;
     z-index: 10;
 }

 .error img {
     width: 100px;
 }
</style>