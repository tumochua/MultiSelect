<template>
  <div class="result-ctn">
    <div v-for="(item, index) in listCheck" :key="index">
      <div class="restlt-item">
        <span>{{ item.name }}</span>
        <span class="result-delete" @click="handleDelete(item.code)">x</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ResultVue",
  props: {
    listCheck: {
      type: Object,
    },
  },
  data() {
    return {};
  },

  created() {
    console.log("check result listChecks : ", this.listCheck);
  },
  methods: {
    handleDelete(data) {
      this.$emit("handleDelete", data);
    },
  },
};
</script>

<style scoped lang="scss">
.result-ctn {
  display: flex;
  border: 1px solid #3333;
  flex-wrap: wrap;
  margin-top: 20px;
  padding: 20px;
  .restlt-item {
    margin-left: 10px;
    .result-delete {
      margin-left: 6px;
      cursor: pointer;
    }
  }
}
</style>
