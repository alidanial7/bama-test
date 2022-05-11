<template>
  <button>{{ text }}</button>
</template>

<script>
export default {
  props: {
    text: {
      type: String,
      required: true,
    },
  },
};
</script>

<style>
button {
  background-color: #06bdb3;
  padding: 10px 30px;
  border: none;
  border-radius: 10px;
  font-weight: bold;
  color: white;
}

button:hover {
  background-color: #06a8a0;
}
</style>
