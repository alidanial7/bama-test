<template>
  <div class="range-input-container">
    <div class="number-box-container">
      <input
        :value="modelValue"
        type="number"
        class="bold subtitle-size"
        @input="$emit('update:modelValue', $event.target.value)"
      />
      <span class="black-color bold subtitle-size ml-2">km</span>
    </div>
    <div>
      <input
        type="range"
        :min="min"
        :max="max"
        :step="step"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
      />
      <div class="box-minmax gray-color">
        <span>{{ min }} km</span><span>{{ max }} km</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    min: {
      type: Number,
      required: true,
    },
    max: {
      type: Number,
      required: true,
    },
    modelValue: {
      type: String,
      required: false,
      default: "0",
    },
    step: {
      type: Number,
      required: false,
      default: 1,
    },
  },
  emits: ["update:modelValue"],
  data: () => {
    return {};
  },
  methods: {},
};
</script>

<style>
@media only screen and (max-width: 600px) {
  input[type="range"] {
    width: 100%;
  }
  .box-minmax {
    width: 100%;
  }
  .range-input-container {
    direction: ltr;
    height: auto;
    display: flex;
    flex-flow: column;
    justify-content: space-evenly;
  }
}
@media only screen and (min-width: 601px) {
  input[type="range"] {
    width: 50%;
  }
  .box-minmax {
    width: 50%;
  }
  .range-input-container {
    direction: ltr;
    height: 450px;
    display: flex;
    flex-flow: column;
    justify-content: space-evenly;
  }
}

input[type="number"] {
  -webkit-appearance: none;
  background-color: #ffffff;
  width: 120px;
  height: 35px;
  border-radius: 10px;
  border: 2px solid #9da1a4;
  text-align: center;
}

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

input[type="range"] {
  display: block;
  -webkit-appearance: none;
  background-color: #bdc3c7;
  height: 5px;
  border-radius: 5px;
  margin: 0 auto;
  outline: 0;
}
input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  background-color: #ffffff;
  width: 25px;
  height: 25px;
  border-radius: 50%;
  border: 2px solid #06bdb3;
  cursor: pointer;
  transition: 0.3s ease-in-out;
}

.box-minmax {
  margin: 10px auto;
  display: flex;
  justify-content: space-between;
  font-size: 20px;
}

.number-box-container {
  display: flex;
  justify-content: center;
  margin: 20px auto;
  align-items: center;
}
</style>
