<template>
  <div class="header">
    <img src="../assets/header.png">
    <div class="navs">
      <button>ABOUT</button>
      <button>SERVICES</button>
      <button>CONTACT</button>
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>
  .header {
    height: 20%;
    width: 80%;
    background-color: #ff7a72;
    position: fixed;
    right: 0;
    top: 0;
  }

  .navs {
    position: fixed;
    top: 7%;
    right: 10%;
  }

  img {
    height: 100%;
    margin-left: 5%
  }

  button {
    margin-left: 2em;
  }
</style>
