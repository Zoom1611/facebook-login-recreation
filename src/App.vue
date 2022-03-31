<template>
  <header>
    <div class="layoutBox">
      <div class="centerMain">
        <div class="main">
          <el-row>
            <el-col :span="16">
              <div class="listOfLogedUsers">
                <img
                  src="./assets/facebook-logo.svg"
                  alt="Facebook Logo"
                  class="facebookLogo"
                />
                <div class="recentLogins">Recent logins</div>
                <div class="clickProfileText">
                  Click your picture or add an account.
                </div>
                <div class="usersAlign">
                  <div
                    class="logedUsers"
                    v-for="(user, index) in listOfUsers"
                    :key="index"
                  >
                    <div class="logedUserBox" @click="openInfo(listOfUsers)">
                      <svg v-html="user.svg" class="clicked"></svg>
                      <div class="nameText">{{ user.firstName }}</div>
                    </div>
                  </div>
                </div>
              </div>
            </el-col>
            <el-col :span="8">
              <div class="loginForm">
                <form action="">
                  <div>
                    <input
                      type="email"
                      name="email"
                      placeholder="Email adress"
                      class="emailInput"
                      v-model="emailInputForLogIn"
                      required
                    />
                    <input
                      type="password"
                      name="password"
                      placeholder="Password"
                      class="passwordInput"
                      v-model="emailInputForPassword"
                      required
                    />
                  </div>
                  <div class="loginButtonBox">
                    <button
                      class="loginButton"
                      @click.prevent="
                        logIn(
                          listOfUsers,
                          emailInputForLogIn,
                          emailInputForPassword
                        )
                      "
                    >
                      Log in
                    </button>
                  </div>
                  <div class="forgotenPasswordBox">
                    <a href="" class="forgottenPassword">Forgotten password?</a>
                  </div>
                  <div class="line"></div>
                </form>
                <div class="createAccountButtonBox">
                  <button class="createAccountButton" @click="createAccount">
                    Create New Account
                  </button>
                </div>
              </div>
            </el-col>
          </el-row>
        </div>
      </div>
    </div>
    <div class="globalContainer"></div>
  </header>
  <SignUp
    v-if="showSignUp"
    @showDialog="closeSignUp"
    @cancelDialog="closeDialog"
  ></SignUp>
  <LogedIn v-if="showLogedIn"></LogedIn>
</template>

<script>
import { createAvatar } from "@dicebear/avatars";
import * as style from "@dicebear/pixel-art";
import SignUp from "./components/SignUp.vue";
import { reactive, ref } from "@vue/reactivity";
import LogedIn from "./components/LogedIn.vue";
export default {
  components: { SignUp, LogedIn },
  setup() {
    const beard = () => {
      let beard = [];
      let variants = ["variant04", "variant03", "variant02", "variant01"];
      beard.push(variants[Math.floor(Math.random() * variants.length)]);
      return beard;
    };

    const beardProbability = () => {
      return Math.floor(Math.random() * (100 - 0 + 1) + 0);
    };

    const eyes = () => {
      let eyes = [];
      let variants = [
        "variant13",
        "variant12",
        "variant11",
        "variant10",
        "variant09",
        "variant08",
        "variant07",
        "variant06",
        "variant05",
        "variant04",
        "variant03",
        "variant02",
        "variant01",
      ];
      eyes.push(variants[Math.floor(Math.random() * variants.length)]);
      return eyes;
    };

    const eyebrows = () => {
      let eyebrows = [];
      let variants = [
        "variant13",
        "variant12",
        "variant11",
        "variant10",
        "variant09",
        "variant08",
        "variant07",
        "variant06",
        "variant05",
        "variant04",
        "variant03",
        "variant02",
        "variant01",
      ];
      eyebrows.push(variants[Math.floor(Math.random() * variants.length)]);
      return eyebrows;
    };

    const mouth = () => {
      let mouth = [];
      let variants = [
        "surprised03",
        "surprised02",
        "happy09",
        "happy08",
        "happy07",
        "happy06",
        "happy05",
        "happy04",
        "happy03",
        "happy02",
        "happy01",
        "surprised01",
      ];
      mouth.push(variants[Math.floor(Math.random() * variants.length)]);
      return mouth;
    };

    const hair = () => {
      let hair = [];
      let variants = [
        "short11",
        "short10",
        "short09",
        "short08",
        "short07",
        "short06",
        "short05",
        "short04",
        "short03",
        "short02",
        "long15",
        "short01",
        "long14",
        "long13",
        "long12",
        "long11",
        "long10",
        "long09",
        "long08",
        "long07",
        "long06",
        "long05",
        "long04",
        "long03",
        "long02",
        "long01",
      ];
      hair.push(variants[Math.floor(Math.random() * variants.length)]);
      return hair;
    };

    const hairProbability = () => {
      return Math.floor(Math.random() * (100 - 30 + 1) + 30);
    };

    const accessories = () => {
      let accessories = [];
      let variants = [
        "variant13",
        "variant12",
        "variant11",
        "variant10",
        "variant09",
        "variant08",
        "variant07",
        "variant06",
        "variant05",
        "variant04",
        "variant03",
        "variant02",
        "variant01",
      ];
      accessories.push(variants[Math.floor(Math.random() * variants.length)]);
      return accessories;
    };

    const accessoriesProbability = () => {
      return Math.floor(Math.random() * (100 - 30 + 1) + 30);
    };

    const glasses = () => {
      let glasses = [];
      let variants = [
        "variant07",
        "variant06",
        "variant05",
        "variant04",
        "variant03",
        "variant02",
        "variant01",
      ];
      glasses.push(variants[Math.floor(Math.random() * variants.length)]);
      return glasses;
    };

    const glassesProbability = () => {
      return Math.floor(Math.random() * (100 - 0 + 1) + 0);
    };

    const hat = () => {
      let hat = [];
      let variants = [
        "variant01",
        "variant02",
        "variant03",
        "variant04",
        "variant05",
        "variant06",
        "variant07",
        "variant08",
        "variant09",
        "variant10",
        "variant11",
        "variant12",
      ];
      hat.push(variants[Math.floor(Math.random() * variants.length)]);
      return hat;
    };

    const clothing = () => {
      let clothing = [];
      let variants = [
        "variant25",
        "variant24",
        "variant23",
        "variant22",
        "variant21",
        "variant20",
        "variant19",
        "variant18",
        "variant17",
        "variant16",
        "variant15",
        "variant14",
        "variant13",
        "variant12",
        "variant11",
        "variant10",
        "variant09",
        "variant08",
        "variant07",
        "variant06",
        "variant05",
        "variant04",
        "variant03",
        "variant02",
        "variant01",
      ];
      clothing.push(variants[Math.floor(Math.random() * variants.length)]);
      return clothing;
    };

    const skincolor = () => {
      let skincolor = [];
      let variants = [
        "variant01",
        "variant02",
        "variant03",
        "variant04",
        "variant05",
        "variant06",
        "variant07",
        "variant08",
      ];
      skincolor.push(variants[Math.floor(Math.random() * variants.length)]);
      return skincolor;
    };

    const hairColor = () => {
      let hairColor = [];
      let variants = [
        "variant01",
        "variant02",
        "variant03",
        "variant04",
        "variant05",
        "variant06",
        "variant07",
        "variant08",
        "variant09",
        "variant10",
      ];
      hairColor.push(variants[Math.floor(Math.random() * variants.length)]);
      return hairColor;
    };

    let svg = ref("");

    const getAvatar = () => {
      svg = createAvatar(style, {
        beard: beard(),
        beardProbability: beardProbability(),
        eyes: eyes(),
        eyebrows: eyebrows(),
        mouth: mouth(),
        hair: hair(),
        hairProbability: hairProbability(),
        accessories: accessories(),
        accessoriesProbability: accessoriesProbability(),
        glasses: glasses(),
        glassesProbability: glassesProbability(),
        hat: hat(),
        hatProbability: 10,
        clothing: clothing(),
        skincolor: skincolor(),
        hairColor: hairColor(),
      });
      return svg;
    };

    let showSignUp = ref(false);
    const createAccount = () => {
      showSignUp.value = true;
    };

    const listOfUsers = reactive([]);

    const closeSignUp = (form) => {
      showSignUp.value = false;
      form.svg = getAvatar();
      listOfUsers.push(form);
      console.log(listOfUsers);
    };

    const closeDialog = () => {
      showSignUp.value = false;
    };

    let showLogedIn = ref(false);
    const logIn = (listOfUsers, email, password) => {
      for (let i = 0; i < listOfUsers.length; i++) {
        if (
          listOfUsers[i].email === email ||
          listOfUsers[i].password === password
        ) {
          showLogedIn.value = true;
        }
      }
    };

    const openInfo = (userInfo) => {
      console.log(userInfo);
    };

    return {
      svg,
      createAccount,
      showSignUp,
      closeSignUp,
      closeDialog,
      listOfUsers,
      logIn,
      showLogedIn,
      openInfo,
    };
  },
};
</script>

<style>
#app {
  font-family: Helvetica, Arial, sans-serif;
}
.layoutBox {
  margin: auto;
  width: 980px;
}
.facebookLogo {
  height: 70px;
  margin: -20px;
}
.centerMain {
  padding-top: 92px;
  padding-bottom: 132px;
}
.main {
  margin: auto;
  width: 980px;
}
.recentLogins {
  margin-top: 15px;
  font-weight: 600;
  font-size: 1.2rem;
}
.clickProfileText {
  font-size: 0.8rem;
}
.logedUserBox {
  border: 1px solid #dddfe2;
  border-radius: 8px;
  width: 190px;
  margin-top: 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-right: 10px;
  cursor: pointer;
}
.logedUserBox:hover {
  box-shadow: 0 0 11px rgba(33, 33, 33, 0.2);
}
.userImg {
  width: 160px;
  padding: 6px;
}
.nameText {
  background-color: #ffffff;
  width: 100%;
  text-align: center;
  padding: 8px;
  border-bottom-left-radius: 8px;
  border-bottom-right-radius: 8px;
}
.usersAlign {
  display: flex;
  width: 600px;
  flex-wrap: wrap;
}

.loginForm {
  margin-top: 35px;
  background-color: #ffffff;
  border: none;
  border-radius: 8px;
  box-shadow: 0 0 11px rgb(33 33 33 / 20%);
  padding: 20px;
  width: 410px;
}
.emailInput {
  padding: 12px;
  border: 1px solid #dddfe2;
  width: 100%;
  border-radius: 4px;
  font-size: 0.85rem;
}

.passwordInput {
  margin-top: 15px;
  padding: 12px;
  border: 1px solid #dddfe2;
  width: 100%;
  border-radius: 4px;
  font-size: 0.85rem;
}
.loginButton {
  padding: 12px;
  border: 1px solid #dddfe2;
  width: 100%;
  border-radius: 8px;
  font-size: 0.95rem;
  color: white;
  text-align: center;
  background-color: #3f77f3;
  margin-top: 15px;
  font-weight: 600;
  cursor: pointer;
}
.loginButton:hover {
  background-color: #2467f7;
}
.forgotenPasswordBox {
  margin-top: 20px;
  text-align: center;
  color: #6abefa;
  font-size: 0.7rem;
}
.forgottenPassword {
  display: inline-block;
  position: relative;
}
.forgottenPassword::after {
  content: "";
  position: absolute;
  width: 100%;
  transform: scaleX(0);
  height: 0.5px;
  bottom: 0;
  left: 0;
  background-color: #02abff;
  transform-origin: bottom right;
  transition: transform 0.25s ease-out;
}
.forgottenPassword:hover:after {
  transform: scaleX(1);
  transform-origin: bottom left;
}
.line {
  border-bottom: 1px solid #dadde1;
  margin-top: 25px;
  margin-bottom: 25px;
}
.createAccountButtonBox {
  display: flex;
  justify-content: center;
}
.createAccountButton {
  padding: 12px;
  border: 1px solid #dddfe2;
  width: 100%;
  border-radius: 8px;
  font-size: 0.85rem;
  color: white;
  text-align: center;
  background-color: #57b82b;
  font-weight: 600;
  cursor: pointer;
  width: 60%;
  margin-bottom: 15px;
}
.createAccountButton:hover {
  background-color: #46a01c;
}
.emailInput::placeholder,
.passwordInput::placeholder {
  color: #9097a2;
}
</style>
