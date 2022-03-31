<template>
  <div class="backdrop">
    <div class="modal">
      <h1 class="header">Congratulation!</h1>
      <p class="paragraph">You are loged in.</p>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
.backdrop {
  top: 0px;
  left: 0px;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
  position: fixed;
}
.modal {
  margin: 100px auto;
  background: white;
  border-radius: 10px;
  width: 800px;
  padding: 20px;
}
.header {
  font-size: 2rem;
  font-weight: bold;
  text-align: center;
  color: #519eff;
  margin-bottom: 20px;
}
.paragraph {
  font-size: 1.2rem;
  margin-bottom: 20px;
  text-align: center;
  color: #a8a8a8;
}
</style>
