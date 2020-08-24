<template>
  <div>
    <label class="custom-checkbox">
      <input
        type="checkbox"
        name="remember-me"
        id="remember-me"
        @change="checkMe"
      />
      <span class="checkbox-label">{{ label }}</span>
    </label>
    <span class="forgotpwd">Forgot Password?</span>
  </div>
</template>

<script>
export default {
  props: {
    label: { type: String, required: true, default: "Remember me" }
  },
  methods: {
    checkMe(e) {
      this.$emit("onRememberMeChange", e.target.checked);
    }
  }
};
</script>

<style scoped>
.forgotpwd {
  margin-left: 50px;
  font-style: italic;
  color: #adabab;
  font-weight: 700;
}
.checkbox-label {
  color: #adabab;
  font-weight: 700;
}
</style>
