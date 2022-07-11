<template>
  <div class="container">
    <h2 class="text-center mt-5 mb-5">USERLY APPLICATION</h2>
    <color-form @setBackgroundColor="setBackgroundColor"></color-form>
    <div class="row userDisplay">
      <arrow-buttons
        :disabled="isDisabledLeft"
        :flag="false"
        @clickHandler="clickHandler"
      ></arrow-buttons>
      <user-cards
        class="col-10 col-sm-5 col-md-5 col-lg-3"
        v-for="randomuser in randomuserData"
        :key="randomuser.id.value"
        :randomuser="randomuser"
        :colorChoiced="colorChoiced"
      ></user-cards>
      <arrow-buttons
        :disabled="isDisabledRight"
        :flag="true"
        @clickHandler="clickHandler"
      ></arrow-buttons>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import ColorForm from "./components/Colorform.vue";
import UserCards from "./components/UserCards.vue";
import arrowButtons from "./components/arrowButtons.vue";

export default {
  name: "App",
  components: {
    ColorForm,
    UserCards,
    arrowButtons,
  },
  data() {
    return {
      colorChoiced:
        localStorage.getItem("colorChoice") != ""
          ? localStorage.getItem("colorChoice")
          : "",
      randomuserData: [],
      windowWidth: "",
      userArrayTotal: [],
      randomBucketSize: 0,
      userArrayLength: 0,
      isDisabledLeft: true,
      isDisabledRight: false,
      iteratorprev: 0,
      iteratornext: 0,
    };
  },
  async mounted() {
    const resp = await axios.get(`https://randomuser.me/api/?results=100`);
    this.userArrayTotal = resp.data.results;
    this.userArrayLength = this.userArrayTotal.length - 1;
    window.addEventListener("resize", this.handleResize);
    this.handleResize();
  },
  unmounted() {
    window.removeEventListener("resize", this.handleResize);
  },
  methods: {
    setBackgroundColor(event) {
      this.colorChoiced = event;
    },
    randomuserDataFormation(windowwidth) {
      this.randomuserData = this.userArrayTotal.slice(0, windowwidth);
      this.iteratornext = this.randomBucketSize;
    },
    handleResize() {
      this.windowWidth = window.innerWidth;
      this.randomuserData = [];
      if (this.windowWidth < 992 && this.windowWidth > 576) {
        this.randomBucketSize = 2;
      } else if (this.windowWidth < 576) {
        this.randomBucketSize = 1;
      } else {
        this.randomBucketSize = 3;
      }

      this.randomuserDataFormation(this.randomBucketSize);
    },
    clickHandler(flag) {
      this.randomuserData = [];
      this.iteratorprev =
        flag == true
          ? this.iteratornext
          : this.iteratorprev - this.randomBucketSize;
      this.iteratornext = this.iteratorprev + this.randomBucketSize;

      this.randomuserData = this.userArrayTotal.slice(
        this.iteratorprev,
        this.iteratornext
      );

      if (flag == true && this.userArrayTotal.length <= this.iteratornext) {
        this.isDisabledRight = true;
      } else if (flag == true && this.iteratorprev > 0) {
        this.isDisabledLeft = false;
      } else if (this.iteratorprev == 0) {
        this.isDisabledRight = false;
        this.isDisabledLeft = true;
      }
    },
  },
};
</script>

<style scopped>
.userDisplay {
  display: flex;
  justify-content: space-between;
}
</style>
