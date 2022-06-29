<template>
  <div>
    <input-select @showHideSelect="showHideSelect"></input-select>
    <list-api-vue
      v-show="showListApi"
      :apiDatas="apiData"
      @handleOk="handleOk"
      @toggleCheckBox="toggleCheckBox"
      @handleCancel="handleCancel"
      v-model="listCheck"
    ></list-api-vue>
    <result-vue
      v-show="showResult"
      :listCheck="listCheck"
      @handleDelete="handleDelete"
    ></result-vue>
  </div>
</template>

<script>
import InputSelect from "./InputSelect.vue";
import ListApiVue from "./ListApi.vue";
import ResultVue from "./Result.vue";

import { mapState, mapGetters } from "vuex";
export default {
  name: "ProvinceVue",
  components: {
    InputSelect,
    ListApiVue,
    ResultVue,
  },
  props: {
    apiData: {
      type: Object,
    },
    result: {
      type: Object,
    },
  },
  data() {
    return {
      showListApi: false,
      showResult: false,
      listCheck: [],
    };
  },
  created() {},
  computed: {
    ...mapState({
      provinces: (state) => state.provinces,
    }),
    ...mapGetters(["getProvince"]),
  },

  methods: {
    handleOk() {
      this.showResult = true;
      this.showListApi = false;
    },
    toggleCheckBox(value) {
      this.listCheck = value;
    },
    handleDelete(code) {
      this.listCheck = this.listCheck.filter((item) => {
        return item.code !== code;
      });
    },
    showHideSelect() {
      this.showListApi = !this.showListApi;
      if (this.listCheck.length > 0) {
        this.showResult = !this.showResult;
      }
    },
    handleCancel() {
      this.showListApi = !this.showListApi;
    },
  },
};
</script>

<style lang="scss" scoped></style>
