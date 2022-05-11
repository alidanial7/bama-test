<template>
  <div class="selectedInfoContainer">
    <span>{{ name }}</span>
    <img
      src="/icons/close.svg"
      alt="close_icon"
      @click="$emit('remove')"
      class="closeIcon"
    />
  </div>
</template>

<script>
export default {
  props: {
    name: {
      type: String,
      required: true,
    },
  },
  emits: ["remove"],
};
</script>

<style>
.selectedInfoContainer {
  border-radius: 5px;
  padding: 5px;
  display: flex;
  justify-content: space-between;
  background-color: rgb(235, 235, 235);
  margin: 5px 0px;
}
.selectedInfoContainer:hover {
  background-color: rgb(219, 218, 218);
}
.closeIcon:hover {
  cursor: pointer;
}
</style>
