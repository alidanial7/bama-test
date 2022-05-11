<template>
  <div class="container">
    <div class="rtl">
      <span class="bold">ماشین حساب | </span>
      <span>محاسبه قیمت خودرو کارکرده</span>
    </div>

    <div class="mt-4" style="display: flex; flex-flow: row-reverse">
      <div class="rtl right-container">
        <p class="subtitle-size-2">بر اساس 875,054 معامله صورت گرفته</p>
        <selected-chip
          v-if="step >= 2"
          :name="selectedBrand.name || ''"
          @remove="removeCarBrand"
        />
        <selected-chip
          v-if="step >= 3"
          :name="selectedModel.name || ''"
          @remove="removeCarModel"
        />
        <selected-chip
          v-if="step >= 4"
          :name="selectedTrim.name || ''"
          @remove="removeCarTrim"
        />
      </div>
      <div class="left-container rtl">
        <p>{{ title }}</p>
        <select-list
          v-if="step === 1"
          :list-items="carBrands"
          :has-header="true"
          @select="selectBrand"
        />

        <select-list
          v-if="step === 2"
          :list-items="carModels"
          :has-header="false"
          @select="selectModel"
        />

        <select-list
          v-if="step === 3"
          :list-items="carTrims"
          :has-header="false"
          @select="selectTrim"
        />

        <range-input
          v-if="step === 4"
          :min="0"
          :max="210000"
          :step="100"
          :default-value="1000"
        />
        <ul>
          <li>
            قیمت خودروها بر اساس پایش، تجمیع و تحلیل قیمت های اعلام شده از سور
            نمایندگی ها، قیمت معاملات انجام شده در بیش از 150 نمایشگاه فعال سطح
            کشور و مراکز خرید و فروش پایتخت و نیز بررسی های میدانی در بازار
            خودرو به صورت روزانه استخراج میشود.
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import cars from "../data/cars";
import RangeInput from "../components/RangeInput.vue";
import SelectedChip from "../components/SelectedChip.vue";
import SelectList from "~~/components/SelectList.vue";

export default {
  components: { RangeInput, SelectedChip, SelectList },
  data() {
    return {
      step: 1,
      carBrands: [],
      carModels: [],
      carTrims: [],

      selectedBrand: null,
      selectedModel: null,
      selectedTrim: null,
    };
  },
  computed: {
    title() {
      switch (this.step) {
        case 1:
          return "برند خودرو را انتخاب کنید:";
        case 2:
          return "مدل خودرو را انتخاب کنید:";
        case 3:
          return "تریم خودرو را انتخاب کنید:";
        case 4:
          return "سال تولید خودرو را انتخاب کنید:";

        default:
          return "";
          break;
      }
    },
  },
  async mounted() {
    let cleanedCarsData = [];
    cars.forEach((element) => {
      cleanedCarsData.push({
        id: element.id,
        name: element.startsWith,
        isHeader: true,
      });
      element.brands.forEach((brand) => {
        cleanedCarsData.push({
          id: brand.id,
          name: brand.name,
          models: brand.models,
          isHeader: false,
        });
      });
    });
    this.carBrands = cleanedCarsData;
  },
  methods: {
    selectBrand(brand) {
      this.selectedBrand = brand;
      this.carModels = this.selectedBrand.models;
      this.step = 2;
    },
    selectModel(model) {
      this.selectedModel = model;
      this.carTrims = this.selectedModel.trims;
      this.step = 3;
    },
    selectTrim(trim) {
      this.selectedTrim = trim;
      this.step = 4;
    },
    removeCarBrand() {
      this.selectedBrand = null;
      this.selectedModel = null;
      this.selectedTrim = null;
      this.step = 1;
    },
    removeCarModel() {
      this.selectedModel = null;
      this.selectedTrim = null;
      this.step = 2;
    },
    removeCarTrim() {
      this.selectedTrim = null;
      this.step = 3;
    },
  },
};
</script>
<style>
.right-container {
  width: 20%;
  border-left: 1px solid rgb(191, 191, 191);
  text-align: justify;
  padding: 10px;
}
.left-container {
  width: 80%;
  padding: 10px;
  min-height: 50px;
  text-align: justify;
}
</style>
