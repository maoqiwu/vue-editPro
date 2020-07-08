<template>
  <div>
    <!-- <div>
      test1 props emit
      <p>{{ bindstr }}</p>
      <button @click="handChangeVal">点我试试啊</button>
    </div>

    <div>
      test2 props emit
      <div>message: {{ value }}</div>
      <button @click="onClick">test</button>
    </div> -->
    <el-dialog :visible.sync="visibleDialog" v-bind="$attrs" v-on="$listeners">
      <!--内容区域的默认插槽-->
      <slot></slot>
      <!--使用弹框的footer插槽添加按钮-->
      <template #footer>
        <!--对外继续暴露footer插槽，有个别弹框按钮需要自定义-->
        <slot name="footer">
          <!--将取消与确定按钮集成到内部-->
          <span>
            <el-button @click="handleCancel">取 消</el-button>
            <el-button type="primary" @click="handleConfirm">
              确 定
            </el-button>
          </span>
        </slot>
      </template>
    </el-dialog>
  </div>
</template>

<script>
import { Dialog } from "element-ui";
export default {
  data() {
    return {};
  },
  // 默认为true，没有在props的定义的属性，将会作为普通的html属性定义在组件的根元素上，设置为false，将传递给$attrs
  inheritAttrs: false,
  props: {
    bindstr: String,
    value: String,
    decimal: {
      type: Number,
      default: 2
    },
    // 对外暴露visible属性，用于显示隐藏弹框
    visible: {
      type: Boolean,
      default: false
    },
    /// 将Dialog的props通过扩展运算符展开到props属性里面
    //但上面的代码存在一定的缺陷，有些组件存在非props的属性，比如对于一些封装的表单组件，我们可能需要给组件传入原生属性，但实际原生属性并没有在组件的props上面定义，这时候，如果通过上面的方式去包装组件，那么这些原生组件将无法传递到内部组件里面。
    ...Dialog.props
  },
  mounted() {
    // console.log(1111);
  },
  computed: {
    // 通过计算属性，对.sync进行转换，外部也可以直接使用visible.sync
    visibleDialog: {
      get() {
        return this.visible;
      },
      set() {
        this.$emit("update:visible");
      }
    }
  },
  methods: {
    handChangeVal() {
      this.$emit("triggerEmit", "hello我 是改变以后的新的参数啊");
    },
    onClick() {
      this.$emit("update:value", "v-model hello我 是改变以后的新的参数啊");
    },
    // 对外抛出cancel事件
    handleCancel() {
      this.$emit("cancel");
    },
    // 对外抛出 confirm事件
    handleConfirm() {
      this.$emit("confirm");
    }
  }
};
</script>
