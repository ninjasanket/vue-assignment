<template>
  <div>
    <input
      :type="type"
      :name="name"
      :id="id"
      :value="value"
      :placeholder="placeholder"
      @input="handleInput"
      @change="handleInput"
      v-bind:class="!isValid ? 'red' : null"
    />
  </div>
</template>

<script>
export default {
  props: {
    type: { type: String, required: true, default: "text" },
    id: { type: String, required: true },
    name: { type: String, required: true },
    value: { type: String, required: false, default: "" },
    label: { type: String, required: true, default: "" },
    placeholder: { type: String },
    isValid: { type: Boolean, default: true }
  },
  methods: {
    handleInput({ target }) {
      if (target.type === "text") {
        this.$emit("onEmailChange", target.value.trim());
      } else if (target.type === "password") {
        this.$emit("onPasswordChange", target.value.trim());
      }
    }
  }
};
</script>
<style scoped>
input {
  padding: 15px;
  min-width: 20%;
  width: 20%;
  border: 2px solid #e0dddd;
  border-radius: 5px;
  margin-bottom: 15px;
}
.red {
  border: 2px solid #ff4343;
}
</style>
