<template>
  <div class="phone-s">
    <div class="phone">
      <div class="phone-top"></div>
      <draggable
        :list="list"
        group="components"
        class="draggableDiv"
      >
        <div
          v-for="(item, i) in list"
          :key="i"
          
          class="content"
        >
        <div v-if="item.componentName == 'VanLayout'">
            <van-layout  :listIndex="i" :cols="list[i].cols"></van-layout>
        </div>
        <component
        @click.native="switchIndex(i)"
         v-else
          class="hoverborder"
          :is="item.componentName"
          :myItem="item"
        ></component>
        </div>
      </draggable>
    </div>
  </div>
</template>
<script>
import draggable from "vuedraggable";
import basicsMixin from "@/common/js/h5/importBasics";
import VanLayout from "@/preview/VanLayout";
import formMixin from "@/common/js/h5/importForm";
import feebackMixin from "@/common/js/h5/importFeeback";
import showMixin from "@/common/js/h5/importShow";
import navMixin from "@/common/js/h5/importNav";
import businessMixin from "@/common/js/h5/importBusiness";
export default {
  mixins: [basicsMixin, formMixin, feebackMixin, showMixin, navMixin, businessMixin],
  components: {
    draggable,
    VanLayout
  },
  computed: {
    list() {
        
      return JSON.parse(localStorage.getItem(this.$route.query.id));
    },
    animateClass() {
      return this.$store.state.rightPanelClass.animateClass;
    },
  },
  data() {
    return {};
  },
  methods: {
    switchIndex: function (index) {
      if (this.animateClass == "myBounceOutRight") {
        // 右边面板由收缩状态变为展开状态
        this.$store.commit("rightPanelFold");
      }

      this.$store.commit("swithIndex", index);
    },
    test: function () {
      console.log("PhoneFrame test")

    }
  },
  mounted() {
      var json = localStorage.getItem(this.$route.query.id);
      console.log(JSON.parse(localStorage.getItem(this.$route.query.id)))
  }
};
</script>
<style lang="scss" scoped>
$phoneWidth: 375px;
$phoneHeight: 667px;

.draggableDiv {
  position: absolute; 
  top: 25px; 
  bottom: 0; 
  left: 0; 
  right: 0;
  // display:flex;
  // flex-wrap: wrap;
  // align-items: flex-start;
  // align-content: flex-start;
}
.phone-s {
  width: $phoneWidth;
  height: $phoneHeight;
  position: relative;
  margin-left: auto;
  margin-right: auto;
  margin-top: 30px;
}
.phone {
  width: $phoneWidth;
  height: $phoneHeight;
  background-color: lightgray;
  position: relative;
  margin-left: auto;
  margin-right: auto;
  overflow-x: hidden;
}
.hoverborder {
  border: 1px solid transparent;
}
.hoverborder:hover {
  border: 1px solid blue;
}
.content{
  padding: 1px;
}
</style>