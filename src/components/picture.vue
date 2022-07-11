<template>
  <picture class="text-center">
    <source media="screen and (min-width:992px)" :srcset="pictureData.large" />
    <source media="screen and (min-width:768px)" :srcset="pictureData.medium" />
    <source
      media="screen and (min-width:576px)"
      :srcset="pictureData.thumbnail"
    />
    <img :src="pictureData.thumbnail" alt="MEN" class="rounded-circle" />
  </picture>
</template>
<script>
export default {
  name: "pictureComponent",
  props: { pictureData: Object },
};
</script>
