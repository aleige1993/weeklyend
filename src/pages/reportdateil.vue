<template>
  <div class="waige">
      <el-breadcrumb separator="/"> 
    <el-breadcrumb-item :to="{ path: '/index/weekreport' }">周报列表</el-breadcrumb-item>
    <el-breadcrumb-item>周某某-周报详情</el-breadcrumb-item>
    </el-breadcrumb>
      <el-tabs v-model="activeName"  type="border-card" style="margin-top:30px">
        <el-tab-pane label="工作总结" name="first">
            <div v-for="o in 4" :key="o" class="fors">
              {{o+'、列表内容 '  }}
            </div> 
        </el-tab-pane>
        <el-tab-pane label="问题与改进措施" name="second" >
            <el-collapse v-model="activeNames"   >
              <el-collapse-item title="一致性 Consistency" name="1">
                <div>与现实生活一致：与现实生活的流程、逻辑保持一致，遵循用户习惯的语言和概念；</div>
                <div>在界面中一致：所有的元素和结构需保持一致，比如：设计样式、图标和文本、元素的位置等。</div>
              </el-collapse-item>
              <el-collapse-item title="反馈 Feedback" name="2">
                <div>控制反馈：通过界面样式和交互动效让用户可以清晰的感知自己的操作；</div>
                <div>页面反馈：操作后，通过页面元素的变化清晰地展现当前状态。</div>
              </el-collapse-item>
              <el-collapse-item title="效率 Efficiency" name="3">
                <div>简化流程：设计简洁直观的操作流程；</div>
                <div>清晰明确：语言表达清晰且表意明确，让用户快速理解进而作出决策；</div>
                <div>帮助用户识别：界面简单直白，让用户快速识别而非回忆，减少用户记忆负担。</div>
              </el-collapse-item>
              <el-collapse-item title="可控 Controllability" name="4">
                <div>用户决策：根据场景可给予用户操作建议或安全提示，但不能代替用户进行决策；</div>
                <div>结果可控：用户可以自由的进行操作，包括撤销、回退和终止当前操作等。</div>
              </el-collapse-item>
            </el-collapse>

        </el-tab-pane>
        <el-tab-pane label="下周工作计划" name="third">
           <div v-for="o in 4" :key="o" class="fors">
              {{o+'、工作计划 '  }}
            </div> 
        </el-tab-pane>
        <el-tab-pane label="批复内容" name="fourth">
          审批内容
        </el-tab-pane>
      </el-tabs>
  </div>
</template>

<script>
export default {
  name: "reportdateil",
  props: [""],
  data() {
    return {
      activeNames:['1','2','3','4'],
      activeName:'first'
    };
  },
  computed: {},

  mounted() {
      console.log(this.$route.params)
  },

  methods: {
    goback(){
        this.$router.go(-1);
    }
  },
};
</script>
<style lang='css' scoped>
.fors{
  margin-top:20px;
}
.tongyi{
/* padding: 30px; */
width: 100%;
}
.conte{
  flex: 1;
}
.tonger span{
  display: inline-block;
  width:25px;
  height: 25px;
  border-radius:100%;
  background-color: #f2f2f2;
  text-align: center;
  line-height: 25px;
  margin-right: 6px;
}
.tonger{
  display: flex;
}
.waige {
  padding: 40px;
}
.marigtop{
  margin-top: 20px;
}
.marigbot{
  margin-bottom: 20px;
}
.rightflex{
  display: flex;
  justify-content: space-between;
}
.pagination{
  text-align: right;
  margin-top: 20px;
}
.modebitsubt{
  margin-top: 20px;
  text-align: right;
  padding-right: 70px;
}
</style>