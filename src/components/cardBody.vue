<template>
  <div class="card-body">
    <h6 class="card-title" v-bind:style="{ 'background-color': color }">
      <i class="fa fa-user"></i>
      {{ `${data.name.title} ${data.name.first} ${data.name.last}` }}
    </h6>
    <p
      class="card-subtitle mb-2 text-muted"
      v-bind:style="{ 'background-color': color }"
    >
      <i class="fa-solid fa-phone"></i>
      {{ data.phone }}
    </p>
    <p
      class="card-subtitle mb-2 text-muted"
      v-bind:style="{ 'background-color': color }"
    >
      <i class="fa-solid fa-at"></i>
      {{ data.email }}
    </p>
    <p
      class="card-subtitle mb-2 text-muted"
      v-bind:style="{ 'background-color': color }"
    >
      <i class="fa-solid fa-location-dot"></i
      >{{
        `${data.location.street.number},${data.location.street.name} ${data.location.city}, ${data.location.state} ${data.location.country} ${data.location.postcode}`
      }}
    </p>
  </div>
</template>
<script>
export default {
  name: "cardBody",
  props: { data: Object, color: String },
};
</script>
<style scoped>
i {
  margin-right: 10px;
}
.card-subtitle {
  font-size: 12px;
}
.card {
  min-height: 300px;
}
</style>
