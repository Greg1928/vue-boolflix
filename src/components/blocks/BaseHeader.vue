<template>
  <header>
    <h1>boolflix</h1>
    <div class="right-part">
      <p>userName</p>
      <i class="fa-solid fa-gift"></i>
      <i class="fa-solid fa-bell"></i>
      <i class="fa-solid fa-circle-user"></i>
      <i class="fa-solid fa-chevron-down chevron"></i>
    </div>
  </header>
</template>

<script>


export default {
    name: "BaseHeader",
  
}
</script>

<style lang="scss" scoped>
header{
  background-color: black;
  height: 80px;
  display: flex;
  justify-content: space-between;

  .right-part{
    color: white;
    display: flex;
    align-items: center;
    font-size: 25px;
    margin-right: 30px;

    & *{
      padding: 0 14px;
      cursor: pointer;
    }
    p{
      margin: 0;
    }
  }

  h1{
  color: red;
  padding: 15px;
  text-transform: uppercase;
  cursor: pointer;
  }
  .chevron{
    font-size: small;
    padding: 0;
  }
}

</style>