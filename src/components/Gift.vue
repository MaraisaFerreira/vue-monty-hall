<template>
  <div class="gift">
      <img src="../assets/imgs/gift.gif">
  </div>
</template>

<script>
export default {
 name: 'Gift'
}
</script>

<style>
 .gift {
     position: relative;
     display: flex;
     align-items: center;
     justify-content: center;
     z-index: 10;
 }

 .gift img {
     width: 100px;
     height: 95px;
 }
</style>