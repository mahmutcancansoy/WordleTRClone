<script setup>


</script>

<template>
  <div id="header">
     <a href="https://www.bundle.app/gundem">
       <img src="public/src/wordle-bundle.png" alt="wordle.tr">
     </a>
    <div class="title">WORDLE TR</div>
    <div class="icons">
      <div class="icon icon-info"></div>
      <div class="icon icon-graph_1"></div>
      <div class="icon icon-setting"></div>
    </div>
  </div>

</template>

<style scoped>
  #header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 11px 16px;
    border-bottom: 1px solid #3a3a3c;
  }
  #header img {
    width: 24px;
    cursor: pointer;
  }
  #header a {
    text-decoration: none;
    color: #575759;
  }
  .title {
    font-weight: 700;
    font-size: 20px;
    text-align: center;
    color: #d7dadc;
    user-select: none;
  }

  .icons {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 19px;

    color: #575759;
  }
 .icon{
   cursor: pointer;
   font-size: 16px;
 }
</style>