<template>
  <div>
    <p>{{ name }}</p>
  </div>
</template>

<script>
export default {
  name: "TableCell",
  props: {
    name: {
      type: String,
      default: "",
    },
  },
};
</script>

<style scoped>
div {
  display: flex;
  align-items: center;
  justify-content: start;
  padding: 4px 0;
}
p {
  padding: 0;
  margin: 0;
}
</style>
