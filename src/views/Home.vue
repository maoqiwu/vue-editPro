<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <!-- <Attr :bindstr="str" @triggerEmit="onMessage" /> -->
    <!-- <Attr :value.sync="message" /> -->
    <button @click="test">
      点击我试试
    </button>
    <Attr
      :visible.sync="visibleDialog"
      title="测试弹框"
      @opened="handleOpened"
      @cancel="handCancel1"
      @confirm="handComfrim1"
      >这是一段内容
    </Attr>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";
import Attr from "@/components/attr";

export default {
  name: "Home",
  data() {
    return {
      str: "fdsfsdfdfs",
      message: "v-mode sync test ",
      visibleDialog: false
    };
  },
  components: {
    // HelloWorld,
    Attr
  },
  methods: {
    onMessage(msg) {
      this.message = msg;
      this.str = msg;
      console.log("接受子组件信息", msg);
    },
    onMessage2(msg) {
      this.str = msg;
      console.log("接受子组件信息", msg);
    },
    handleOpened(e) {
      console.log("窗口它打开了");
    },
    test() {
      this.visibleDialog = !this.visibleDialog;
    },
    handCancel1() {
      console.log("handCancel");
    },
    handComfrim1() {
      console.log("handComfrim");
    }
  }
};
</script>
