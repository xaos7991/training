<template>
  <div :class="$style.root">
    <h5 :class="$style.title">{{ title }}</h5>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: true,
    },
  },
};
</script>

<style module>
.root {
  background: white;
  padding: 5px;
  border-radius: 5px;
  margin-bottom: 5px;
}

.title {
  margin: 0;
}
</style>
