<template>
  <div>
    <div class="list-api">
      <div class="list-select">
        <div v-for="apiData in apiDatas" :key="apiData.code">
          <label class="list-checkbox">
            <input
              class="check-box-input"
              type="checkbox"
              :value="apiData"
              v-model="listApi"
            />
            {{ apiData.name }}
          </label>
        </div>
      </div>
    </div>
    <div class="btn-ctn">
      <button
        @click="handleOk()"
        :class="listApi.length > 0 ? 'btn-ok' : 'btn-disble'"
      >
        Đồng ý
      </button>
      <!-- <button @click="handleOk()" class="btn-ok">Đồng ý</button> -->
      <button @click="handleCancel()" class="btn-cancel">Hủy</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ListApi",
  props: {
    apiDatas: {
      type: Object,
    },
    modelValue: Array,
  },
  data() {
    return {
      listApi: [],
    };
  },
  created() {},
  methods: {
    handleOk() {
      this.$emit("handleOk");
    },
    handleCancel() {
      this.$emit("handleCancel");
    },
  },
  watch: {
    listApi: function (value) {
      this.$emit("toggleCheckBox", value);
    },
    modelValue: function (val) {
      this.listApi = val;
    },
  },
};
</script>

<style scoped lang="scss">
.list-api {
  background-color: #ffff;
  overflow-y: scroll;
  .list-select {
    height: 304px;
    border-radius: 4px;
    margin: 0 auto;
    .list-checkbox {
      padding: 7px;
      text-align: left;
      display: flex;
      align-items: center;
      cursor: pointer;
      &:hover {
        background-color: #e7f1fd;
      }
      .check-box-input {
        width: 16px;
        height: 16px;
        margin-right: 12px;
      }
    }
  }
}
.btn-ctn {
  text-align: left;
  .btn-ok {
    left: 10px;
    background-color: #007bc3;
    cursor: pointer;
    text-align: center;
    border: none;
    font-weight: 700;
    color: rgba(255, 255, 255, 1);
    width: 104px;
    height: 32px;
    border-radius: 6px;
  }
  .btn-disble {
    pointer-events: none;
    left: 10px;
    background-color: #dcdcdc;
    text-align: center;
    border: none;
    font-weight: 700;
    color: rgba(255, 255, 255, 1);
    width: 104px;
    height: 32px;
    border-radius: 6px;
  }
}
.btn-cancel {
  right: 0px;
  border: none;
  background-color: #fff;
  color: #007bc3;
  font-weight: 400;
  font-size: 16px;
  width: 82px;
  height: 24px;
  cursor: pointer;
}
::-webkit-scrollbar {
  width: 8px;
  height: 62px;
  border-radius: 6px;
}
::-webkit-scrollbar-thumb {
  background: #dcdcdc;
  width: 8px;
  height: 62px;
  border-radius: 6px;
}
</style>
