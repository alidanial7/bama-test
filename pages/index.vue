<template>
  <div class="container">
    <div class="rtl">
      <span class="bold">ماشین حساب | </span>
      <span>محاسبه قیمت خودرو کارکرده</span>
    </div>

    <div class="mt-4 page-container">
      <div class="rtl right-container">
        <p class="subtitle-size-2">بر اساس 875,054 معامله صورت گرفته</p>
        <div>
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
          <selected-chip
            v-if="step >= 5"
            :name="selectedYear.name || ''"
            @remove="removeCarYear"
          />
          <p class="subtitle-size-2">کارکرد</p>
          <selected-chip
            v-if="step >= 5"
            :name="`${selectedDistance} کیلومتر`"
            @remove="removeCarDistance"
          />
        </div>
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

        <select-list
          v-if="step === 4"
          :list-items="carYears"
          :has-header="false"
          @select="selectYear"
        />

        <range-input
          v-if="step === 5"
          v-model="selectedDistance"
          :min="0"
          :max="210000"
          :step="100"
        />
        <div v-if="step === 5" class="button-container">
          <theme-button text="ادامه" />
        </div>
        <div>
          <ul>
            <li>
              قیمت خودروها بر اساس پایش، تجمیع و تحلیل قیمت های اعلام شده از سور
              نمایندگی ها، قیمت معاملات انجام شده در بیش از 150 نمایشگاه فعال
              سطح کشور و مراکز خرید و فروش پایتخت و نیز بررسی های میدانی در
              بازار خودرو به صورت روزانه استخراج میشود.
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import cars from "../data/cars";
import RangeInput from "../components/RangeInput.vue";
import SelectedChip from "../components/SelectedChip.vue";
import SelectList from "~~/components/SelectList.vue";
import ThemeButton from "~~/components/ThemeButton.vue";

export default {
  components: { RangeInput, SelectedChip, SelectList, ThemeButton },
  data() {
    return {
      step: 1,
      carBrands: [],
      carModels: [],
      carTrims: [],
      carYears: [],

      selectedBrand: null,
      selectedModel: null,
      selectedTrim: null,
      selectedYear: null,
      selectedDistance: "10000",
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
        case 5:
          return "کارکرد خودرو را وارد کنید:";

        default:
          return "";
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
      this.carYears = this.selectedTrim.years;
      this.step = 4;
    },
    selectYear(year) {
      this.selectedYear = year;
      this.step = 5;
    },
    removeCarBrand() {
      this.selectedBrand = null;
      this.selectedModel = null;
      this.selectedTrim = null;
      this.selectedYear = null;
      this.step = 1;
    },
    removeCarModel() {
      this.selectedModel = null;
      this.selectedTrim = null;
      this.selectedYear = null;
      this.step = 2;
    },
    removeCarTrim() {
      this.selectedTrim = null;
      this.selectedYear = null;
      this.step = 3;
    },
    removeCarYear() {
      this.selectedYear = null;
      this.step = 4;
    },
    removeCarDistance() {
      this.selectedYear = null;
      this.selectedDistance = "10000";
      this.step = 4;
    },
  },
};
</script>
<style>
@media only screen and (max-width: 600px) {
  .page-container {
    display: flex;
    flex-flow: column;
  }
  .right-container {
    width: 100%;
    text-align: justify;
  }
  .range-input-container {
    direction: ltr;
    display: flex;
    flex-flow: column;
    justify-content: flex-start;
  }
  .left-container {
    max-height: 50px;
    text-align: justify;
  }
}
@media only screen and (min-width: 601px) {
  .page-container {
    display: flex;
    flex-flow: row-reverse;
  }
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
  .button-container {
    display: flex;
    flex-flow: row-reverse;
  }
}
</style>
