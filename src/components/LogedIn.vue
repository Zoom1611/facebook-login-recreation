<template>
  <div class="backdrop">
    <div class="modal">
      <h1 class="header">Congratulation!</h1>
      <p class="paragraph">You are loged in.</p>
      <div class="signUpLine"></div>
      <el-row :gutter="20">
        <el-col :span="8">
          <div class="userBox">
            <svg v-html="logedUser.svg"></svg>
          </div>
        </el-col>
        <el-col :span="16" class="aboutUser">
          <div>
            <span class="infoTextDesign">Username: </span
            ><span class="dynamicUserInfo">{{ logedUser.firstName }}</span>
          </div>
          <div>
            <span class="infoTextDesign">Lastname: </span
            ><span class="dynamicUserInfo">{{ logedUser.lastName }}</span>
          </div>
          <div>
            <span class="infoTextDesign">Email: </span
            ><span class="dynamicUserInfo">{{ logedUser.email }}</span>
          </div>
          <div>
            <span class="infoTextDesign">Gender: </span
            ><span class="dynamicUserInfo">{{ logedUser.gender }}</span>
          </div>
        </el-col>
      </el-row>
      <div class="closeButtonBox">
        <el-button @click="closeLogedIn" size="large">Close</el-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Loged in",
  props: ["logedUser"],
  setup(props, context) {
    console.log(props.logedUser);

    const closeLogedIn = () => {
      context.emit("closeLogedIn", null);
    };

    return { closeLogedIn };
  },
};
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
  padding: 25px 50px;
}
.header {
  font-size: 2rem;
  font-weight: bold;
  text-align: center;
  color: #519eff;
  margin-bottom: 10px;
}
.paragraph {
  font-size: 1.2rem;
  margin-bottom: 20px;
  text-align: center;
  color: #a8a8a8;
}
.userBox {
  border: 1px solid #dddfe2;
  border-radius: 8px;
  width: 220px;
  height: 220px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.aboutUser {
  font-size: 0.9rem;
}
.infoTextDesign {
  color: #a8a8a8;
}
.dynamicUserInfo {
  color: #85bcff;
}
.closeButtonBox {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}
</style>
