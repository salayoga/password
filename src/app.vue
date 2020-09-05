
<template>
  <!-- 6位密码输入框 -->
  <div class="password">
    <input class="hideInput" type="number" :value="value" @input="handlechange" />
    <div
      :class="['input',value[index]?'activeContent':activeIndex==index?'activeInsert':'',activeIndex==num-1 && index==num-1?'active':'']"
      v-for="(item,index) of divArr"
      :key="index"
      @click="handlechoose($event,index)"
      :style="{'width':width+'px','height':width+'px','border-color':borderColor}"
    ></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeIndex: -1,
      event: null,
      divArr: [],
    };
  },
  props: {
    width: {
      type: Number,
    },
    num: {
      type: Number,
      default: 6,
    },
    value: {
      type: String,
    },
    borderColor: {
      type: String,
    },
  },
  mounted() {
    this.divArr = new Array(this.num);
    window.addEventListener("click", (e) => {
      this.changeActiveIndex(e);
    });
    this.$once("hook:beforeDestroy", () => {
      window.removeEventListener("click", (e) => {
        this.changeActiveIndex(e);
      });
    });
  },
  methods: {
    //点击空白处自动失焦
    changeActiveIndex(e) {
      if (e != this.event) {
        this.activeIndex = -1;
      }
    },
    //点击输入框获取最小空白框和输入框聚焦
    handlechoose(e) {
      this.event = e;
      let valueLength = this.value.length;
      if (valueLength > this.num - 1) {
        this.activeIndex = this.num - 1;
      } else {
        this.activeIndex = valueLength;
      }
      e.target.parentNode.querySelector(".hideInput").focus();
    },
    handlechange(e) {
      let value = e.target.value;
      let valueLength = value.length;
      if (value.slice(-2, -1) >= 0 && value.slice(-2, -1) <= 9) {
        if (valueLength > this.num - 1) {
          value = value.slice(0, this.num);
          this.activeIndex = this.num - 1;
        } else {
          this.activeIndex = value.length;
        }
      }
      e.target.value = value;
      this.$emit("input", value);
    },
  },
};
</script>   

<style lang="less" scoped>
.password {
  display: flex;
  margin-top: 7px;
  position: relative;
  .hideInput {
    position: absolute;
    left: 600px;
    width: 0;
    height: 0;
    border: 0;
    outline: 0;
  }
  .input {
    width: 25px;
    height: 25px;
    display: block;
    border: 1px solid #ccc;
    text-align: center;
    outline: none;
    padding: 0;
    cursor: text;
  }
  .input:not(:last-child) {
    border-right: 0;
  }
  .activeInsert {
    position: relative;
    box-shadow: inset 0 0 1px 1px #2176ff;
    &:after {
      content: "";
      position: absolute;
      width: 1px;
      height: 70%;
      left: 50%;
      top: 15%;
      background: #000;
    }
  }
  .active {
    position: relative;
    box-shadow: inset 0 0 1px 1px #2176ff;
  }
  .activeContent {
    position: relative;
    &:after {
      content: "";
      position: absolute;
      width: 4px;
      height: 4px;
      border-radius: 50%;
      background: #000;
      top: 50%;
      left: 50%;
      transform: translate(-2px, -2px);
    }
  }
}
</style>