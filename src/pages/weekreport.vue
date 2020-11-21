<template>
  <div class="waige">
    <el-row>
      <el-col>
        <div class="rightflex marigbot">
          <div>
            <el-button type="primary" @click="adduser()" size="small"
              ><i class="el-icon-download"></i> 周报下载</el-button
            >
          </div>
          <div>
            <el-input
            style="width: 200px"
            size="small"
            placeholder="输入姓名检索"
          ></el-input>
          <el-button type="primary" size="small" @click="onSOSO"
            >搜索</el-button
          >
          </div>
          
        </div>
      </el-col>
    </el-row>
    <div class="biaoge">
      <el-row>
        <el-col>
          <el-table :header-cell-style="{ background: '#fafafa' }" :data="tableData" size="small" border style="width: 100%">
               <el-table-column  type="selection"
      width="42"></el-table-column>
            <el-table-column
              v-for="(item, index) in columnData"
              :key="index"
              :prop="item.prop"
              :label="item.label"
              :min-width="item.width"
            >
              <template slot-scope="scope">
                <div v-if="item.prop == 'opention'">
                  <el-button
                    @click="clickRow(scope.row)"
                    type="warning"
                    size="small"
                    icon="el-icon-sort"
                    >查看详情</el-button
                  >
                  <el-popconfirm
                    confirm-button-text="确定"
                    cancel-button-text="取消"
                    icon="el-icon-info"
                    icon-color="red"
                    title="确定删除吗？"
                    @confirm="deltRow(scope.row)"
                  >
                    <el-button
                      slot="reference"
                      type="danger"
                      size="small"
                      icon="el-icon-delete"
                      >删除</el-button
                    >
                  </el-popconfirm>
                </div>
              </template>
            </el-table-column>
          </el-table>
        </el-col>
      </el-row>
        
          <div class="pagination">
            <el-pagination background layout="prev, pager, next" :total="600">
          </el-pagination>
          </div> 
    </div>

    <el-dialog
      title="周报详情"
      :visible.sync="drawer"
      width="50%"
      :before-close="drawerClose">
       <el-tabs v-model="activeName" >
        <el-tab-pane label="工作总结" name="first">
            <div v-for="o in 4" :key="o" class="fors">
              {{o+'、列表内容 '  }}
            </div> 
        </el-tab-pane>
        <el-tab-pane label="问题与改进措施" name="second">
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
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: "weekreport",
  props: [""],
  data() {
    return {
      activeNames:['1','2','3','4'],
      activeName:'first',
      isAdd:true,
      drawer: false,
      tableData: [
        {
          name: "1231231231",
          date: "1231231231",
          status1: "1231231231",
          status2: "1231231231",
          checkUser: "1231231231", 
        },
      ],
      columnData: [
        {
          label: "姓名",
          prop: "name",
          width: "40%",
        },
        {
          label: "提交时间",
          prop: "date",
          width: "40%",
        },
        {
          label: "周报状态",
          prop: "status1",
          width: "40%",
        },
        {
          label: "批复状态",
          prop: "status2",
          width: "40%",
        },
         {
          label: "审批人",
          prop: "checkUser",
          width: "40%",
        },
        {
          label: "操作",
          width: "",
          prop: "opention",
        },
      ],
    };
  },
  computed: {},

  mounted() {},

  methods: {
    onSOSO() {},
    adduser() {
      this.isAdd = true
      this.drawer = true;
    },
    drawerClose() {
      this.drawer = false;
    },
    clickRow(scope) {
      this.drawer = true;
      this.isAdd = false
    },
    deltRow(scope) {
      console.log(scope);
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