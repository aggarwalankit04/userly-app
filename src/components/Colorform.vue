<template>
  <form class="row form-inline user-form">
    <div class="form-group col-6 col-sm-4 col-md-4 col-lg-4 mb-5">
      <input
        type="color"
        class="form-control"
        placeholder="choose color"
        v-model="colorChoiced"
        v-on:change="changeBackgroundColor"
      />
    </div>
  </form>
</template>

<script>
export default {
  name: "ColorForm",
  data() {
    return {
      colorChoiced:
        localStorage.getItem("colorChoice") != ""
          ? localStorage.getItem("colorChoice")
          : "",
    };
  },
  methods: {
    changeBackgroundColor() {
      if (!this.colorChoiced) {
        alert("Select Any color");
        return;
      }
      localStorage.setItem("colorChoice", this.colorChoiced);
      this.$emit("setBackgroundColor", this.colorChoiced);
    },
  },
};
</script>
<style scoped>
.user-form {
  display: flex;
  align-items: baseline;
  justify-content: center;
}
</style>
