<template>
  <div class="container">
    <h2 class="text-center mt-5 mb-5">USERLY APPLICATION</h2>
    <ColorForm @setBackgroundColor="setBackgroundColor"></ColorForm>
    <div class="row userDisplay">
      <div class="col-1 col-sm-1 col-md-1 col-lg-1 arrow-left">
        <i
          class="fa-solid fa-arrow-left"
          :class="{ disabled: isDisabledLeft }"
          @click="prevClick"
        ></i>
      </div>

      <div
        class="col-10 col-sm-5 col-md-5 col-lg-3"
        v-for="randomuser in randomuserData"
        :key="randomuser.id.value"
      >
        <user-cards
          :randomuser="randomuser"
          :colorChoiced="colorChoiced"
        ></user-cards>
      </div>

      <div class="col-1 col-sm-1 col-md-1 col-lg-1 arrow-right">
        <i
          class="fa-solid fa-arrow-right"
          :class="{ disabled: isDisabledRight }"
          @click="nextClick"
        ></i>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
import ColorForm from "./components/Colorform.vue";
import UserCards from "./components/UserCards.vue";

export default {
  name: "App",
  components: {
    ColorForm,
    UserCards,
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
      console.log(event);
      if (!event) {
        alert("Select Any color");
        return;
      }
      this.colorChoiced = event;
      localStorage.setItem("colorChoice", this.colorChoiced);
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
        this.randomuserDataFormation(this.randomBucketSize);
      } else if (this.windowWidth < 576) {
        this.randomBucketSize = 1;
        this.randomuserDataFormation(this.randomBucketSize);
      } else {
        this.randomBucketSize = 3;
        this.randomuserDataFormation(this.randomBucketSize);
      }
    },
    prevClick() {
      this.randomuserData = [];
      this.iteratornext = this.iteratorprev;
      this.iteratorprev = this.iteratorprev - this.randomBucketSize;
      this.randomuserData = this.userArrayTotal.slice(
        this.iteratorprev,
        this.iteratornext
      );
      if (this.iteratorprev == 0) {
        this.isDisabledRight = false;
        this.isDisabledLeft = true;
      }
    },
    nextClick() {
      this.randomuserData = [];
      this.iteratorprev = this.iteratornext;
      this.iteratornext = this.iteratorprev + this.randomBucketSize;
      this.randomuserData = this.userArrayTotal.slice(
        this.iteratorprev,
        this.iteratornext
      );

      if (this.userArrayTotal.length <= this.iteratornext) {
        this.isDisabledRight = true;
      } else if (this.iteratorprev > 0) {
        this.isDisabledLeft = false;
      }
    },
  },
};
</script>

<style scoped>
i {
  margin-right: 10px;
}

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

.userDisplay {
  display: flex;
  justify-content: space-between;
}
.card-subtitle {
  font-size: 12px;
}
.card {
  min-height: 300px;
}
.user-form {
  display: flex;
  align-items: baseline;
  justify-content: center;
}
.disabled {
  display: none;
}
</style>
