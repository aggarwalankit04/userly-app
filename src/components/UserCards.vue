<template>
  <div class="card">
    <picture-component :picture-data="randomuser.picture"></picture-component>
    <card-body :data="randomuser" :color="colorChoiced"></card-body>
  </div>
</template>

<script>
import pictureComponent from "./picture.vue";
import cardBody from "./cardBody.vue";
export default {
  name: "UserCards",
  props: { randomuser: Object, colorChoiced: String },
  components: {
    pictureComponent,
    cardBody,
  },
};
</script>
