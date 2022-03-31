<template>
  <div class="backdrop">
    <div class="modal">
      <h1 class="signUpHeader">Sign up</h1>
      <p class="para">It's quick and easy!</p>
      <div class="signUpLine"></div>
      <div>
        <el-form
          :model="form"
          label-width="120px"
          :rules="rules"
          ref="ruleFormRef"
        >
          <el-form-item label="First name" prop="firstName">
            <el-input v-model="form.firstName" />
          </el-form-item>
          <el-form-item label="Last name" prop="lastName">
            <el-input v-model="form.lastName" />
          </el-form-item>
          <el-form-item label="Email" prop="email">
            <el-input v-model="form.email" type="email" autocomplete="off" />
          </el-form-item>
          <el-form-item label="Password" prop="password">
            <el-input
              v-model="form.password"
              type="password"
              autocomplete="off"
            />
          </el-form-item>
          <el-form-item label="Confirm" prop="checkPassword">
            <el-input
              v-model="form.checkPassword"
              type="password"
              autocomplete="off"
            />
          </el-form-item>

          <el-form-item label="Gender" prop="gender">
            <el-radio-group v-model="form.gender">
              <el-radio label="Male" />
              <el-radio label="Female" />
            </el-radio-group>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="onSubmit(form, ruleFormRef)"
              >Sign Up</el-button
            >
            <el-button @click="onCancel">Cancel</el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, ref } from "@vue/reactivity";

export default {
  emits: ["showDialog", "cancelDialog"],
  setup(props, context) {
    const form = reactive({
      firstName: "",
      lastName: "",
      email: "",
      password: "",
      checkPassword: "",
      gender: "",
      svg: "",
    });

    let ruleFormRef = ref("");

    const onSubmit = async (form, ruleFormRef) => {
      if (!ruleFormRef) return;
      await ruleFormRef.validate((valid) => {
        if (valid) {
          context.emit("showDialog", form);
        }
      });
    };

    const onCancel = () => {
      context.emit("cancelDialog", form);
    };

    const validatePass = (value, callback) => {
      if (value === "") {
        callback(new Error("Please input the password"));
      } else {
        if (form.checkPassword !== "") {
          if (!ruleFormRef.value) return;
          ruleFormRef.value.validateField("checkPass", () => null);
        }
        callback();
      }
    };

    const validatePass2 = (value, callback) => {
      if (value === "") {
        callback(new Error("Please input the password again"));
      } else if (value !== form.password) {
        callback(new Error("Two inputs don't match!"));
      } else {
        callback();
      }
    };

    const rules = reactive({
      firstName: [
        {
          required: true,
          message: "Please input firstname",
          trigger: "blur",
        },
      ],
      lastName: [
        {
          required: true,
          message: "Please input lastname",
          trigger: "blur",
        },
      ],
      email: [
        {
          required: true,
          message: "Please input email",
          trigger: "blur",
        },
      ],
      password: [
        {
          required: true,
          validator: validatePass,
          trigger: "blur",
        },
      ],
      checkPassword: [
        {
          required: true,
          validator: validatePass2,
          trigger: "blur",
        },
      ],
      gender: [
        {
          required: true,
          message: "Please select gender",
          trigger: "change",
        },
      ],
    });

    return { form, onSubmit, onCancel, rules, ruleFormRef };
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
  width: 600px;
  padding: 20px;
}
.signUpHeader {
  font-size: 1.5rem;
  margin-bottom: 8px;
  text-align: center;
  font-weight: bold;
  color: #519eff;
}
.para {
  font-size: 0.8rem;
  margin-bottom: 20px;
  text-align: center;
  color: #a8a8a8;
}
.signUpLine {
  border-bottom: 1px solid #dadde1;
  margin-bottom: 20px;
}
.firstName,
.lastName {
  padding: 12px;
  border: 1px solid #dddfe2;
  border-radius: 4px;
  font-size: 0.85rem;
  width: 100%;
  margin-bottom: 10px;
}
.email,
.password {
  padding: 12px;
  border: 1px solid #dddfe2;
  width: 100%;
  border-radius: 4px;
  font-size: 0.85rem;
}
.email {
  margin-bottom: 10px;
}
.firstName::placeholder,
.lastName::placeholder,
.email::placeholder,
.password::placeholder {
  color: #9097a2;
}
</style>
