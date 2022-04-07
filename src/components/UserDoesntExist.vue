<template>
  <div class="backdrop">
    <div class="modal">
      <div class="messageForWrongInput">Wrong Email or Password!</div>
      <p class="tryAgain">Retype it and try again.</p>
      <div class="closeButtonBox" @click="closeMessageForWrongInput">
        <el-button type="info" plain size="large">Close</el-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Wrong Email or Password",
  setup(props, context) {
    const closeMessageForWrongInput = () => {
      context.emit("closeMessageForWrongInput", null);
    };

    return { closeMessageForWrongInput };
  },
};
</script>

<style>
.messageForWrongInput {
  font-size: 2rem;
  color: #ff5151;
  margin: 20px;
  text-align: center;
}
.tryAgain {
  margin: 40px 20px;
  text-align: center;
  font-size: 1.2rem;
  color: #a8a8a8;
}
.buttonCloseTryAgain {
  color: #a8a8a8;
  width: 200px;
}
</style>
