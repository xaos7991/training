<template>
  <div :class="$style.root">
    <h4 :class="$style.title">{{ title }}</h4>
    <slot />
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
  background-color: mediumseagreen;
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 5px;
}

.title {
  margin-top: 0;
  color: white;
}
</style>
