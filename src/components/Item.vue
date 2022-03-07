<template>
  <div class="item">
    <p class="title">
      {{ content.name }}
    </p>
    <p class="description">
      {{ content.description }}
    </p>
    <a v-bind:href="content.url">{{ content.url }}</a>
  </div>
</template>

<script>
export default {
  name: "ListItem",
  props: {
    content: Object,
  },
};
</script>

<style scoped>
.item {
  border: 1px solid #f2f2f2;
  text-align: left;
  padding: 1% 3%;
  background-color: white;
  margin: 1rem;
}

.title {
  color: black;
  font-weight: bolder;
  font-size: 1.6rem;
}
</style>
