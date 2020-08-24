<template>
  <div id="login-container">
    <div>
      <span>{{ loginText }}</span>
      <form @submit.prevent="onSubmit">
        <div>
          <app-textbox-component
            type="text"
            v-model="userEmail"
            placeholder="Username"
            label="Enter name"
            id="email"
            name="email"
            :isValid="isValidEmailInput"
            @onEmailChange="onEmailChange($event)"
          />
          <app-textbox-component
            type="password"
            v-model="userPassword"
            placeholder="Password"
            label="Enter password"
            id="password"
            name="password"
            :isValid="isValidPasswordInput"
            @onPasswordChange="onPasswordChange($event)"
          />
          <app-checkbox-component
            label="Remember me"
            @onRememberMeChange="onRememberMeChange($event)"
          ></app-checkbox-component>
          <div>
            <button type="submit" v-if="isShow">Login</button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

import textBoxComponent from "./textBoxComponent";
import checkBoxComponent from "./checkBoxComponent";

export default {
  components: {
    "app-textbox-component": textBoxComponent,
    "app-checkbox-component": checkBoxComponent
  },
  data() {
    return {
      loginText: "Member Login",
      userEmail: "",
      userPassword: "",
      isRememberMeSelected: false,
      isValidEmailInput: true,
      isValidPasswordInput: true,
      isShow: true
    };
  },
  computed: {
    isEmailValid() {
      return this.isEmailValid ? true : false;
    },
    isPasswordValid() {
      return this.isValidPasswordInput ? true : false;
    }
  },
  methods: {
    onEmailChange(email) {
      this.userEmail = email;
    },
    onPasswordChange(passowrd) {
      this.userPassword = passowrd;
    },
    onRememberMeChange(isSelected) {
      this.isRememberMeSelected = isSelected;
    },
    onSubmit() {
      const isValid = this.validateForm();
      console.log("isValid :: ", isValid);
      const formData = {
        userEmail: this.userEmail,
        userPassword: this.userPassword,
        isRememberMeSelected: this.isRememberMeSelected
      };

      if (!isValid) return;

      this.isShow = false;
      axios
        .post("https://vue-http-d3dd4.firebaseio.com/user.json", formData)
        .then(res => {
          this.isShow = true;
          alert("Form Submitted Successfully!");
          this.userPassword = this.userEmail = "";
        })
        .catch(e => {
          this.isShow = true;
        });
    },
    validateForm() {
      const pattern = /^[a-z0-9]+@[a-z]+\.[a-zA-Z]{3}$/;
      this.isValidPasswordInput = this.isValidEmailInput = true;

      if (!pattern.test(this.userEmail)) {
        this.isValidEmailInput = false;
      }
      if (this.userPassword.length <= 5) {
        this.isValidPasswordInput = false;
      }
      return this.isValidEmailInput && this.isValidPasswordInput ? true : false;
    }
  }
};
</script>

<style scoped>
span {
  font-weight: 600;
  font-size: 22px;
  color: #635f5f;
}
form {
  margin-top: 20px;
}
button {
  width: 10%;
  padding: 7px 0px 7px 0px;
  background-color: #ec8f1dbd;
  border-color: #ec8f1dbd;
  border-radius: 5px;
  box-shadow: none;
  margin-top: 15px;
  margin-left: -175px;
  color: white;
  font-size: larger;
}
</style>
