<template>
  <div class="card">
    <picture class="text-center">
      <source
        media="screen and (min-width:992px)"
        :srcset="randomuser.picture.large"
      />
      <source
        media="screen and (min-width:768px)"
        :srcset="randomuser.picture.medium"
      />
      <source
        media="screen and (min-width:576px)"
        :srcset="randomuser.picture.thumbnail"
      />
      <img
        :src="randomuser.picture.thumbnail"
        alt="MEN"
        class="rounded-circle"
      />
    </picture>
    <div class="card-body">
      <h6
        class="card-title"
        v-bind:style="{ 'background-color': colorChoiced }"
      >
        <i class="fa fa-user"></i>
        {{
          `${randomuser.name.title} ${randomuser.name.first} ${randomuser.name.last}`
        }}
      </h6>
      <p
        class="card-subtitle mb-2 text-muted"
        v-bind:style="{ 'background-color': colorChoiced }"
      >
        <i class="fa-solid fa-phone"></i>
        {{ randomuser.phone }}
      </p>
      <p
        class="card-subtitle mb-2 text-muted"
        v-bind:style="{ 'background-color': colorChoiced }"
      >
        <i class="fa-solid fa-at"></i>
        {{ randomuser.email }}
      </p>
      <p
        class="card-subtitle mb-2 text-muted"
        v-bind:style="{ 'background-color': colorChoiced }"
      >
        <i class="fa-solid fa-location-dot"></i
        >{{
          `${randomuser.location.street.number},${randomuser.location.street.name} ${randomuser.location.city}, ${randomuser.location.state} ${randomuser.location.country} ${randomuser.location.postcode}`
        }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserCards",
  props: { randomuser: Object, colorChoiced: String },
};
</script>
