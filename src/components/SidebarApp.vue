<template>
  <div class="Sidebar">
    <div class="logo"></div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="scss">
.Sidebar {
  z-index: 2;
  background-color: #16b1f7;
  width: 5.5vw;
  border-radius: 1.5em;

  .logo {
    height: 20%;

    background-image: url("https://seeklogo.com/images/H/healthcare-hospital-logo-3FD591E41F-seeklogo.com.png");
    background-repeat: no-repeat;
    background-size: 80%;
    background-position: center;
  }
}
</style>
