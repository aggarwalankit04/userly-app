<template>
  <div class="col-1 col-sm-1 col-md-1 col-lg-1 arrow-right">
    <i
      class="fa-solid"
      :class="[{ disabled: disabled }, arrowDirection]"
      @click="clickHandler()"
    ></i>
  </div>
</template>
<script>
export default {
  name: "arrowButtons",
  props: { disabled: Boolean, flag: Boolean },
  data() {
    return {
      arrowDirection: this.flag ? "fa-arrow-right" : "fa-arrow-left",
    };
  },
  methods: {
    clickHandler() {
      this.$emit("clickHandler", this.flag);
    },
  },
};
</script>
<style scoped>
.arrow-left {
  display: flex;
  align-items: center;
  justify-content: flex-end;
}

.arrow-right {
  display: flex;
  align-items: center;
  justify-content: flex-start;
}

.disabled {
  display: none;
}
</style>
