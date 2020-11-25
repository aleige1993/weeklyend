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
          label: "审批人",
          prop: "checkUser",
          width: "40%",
        },
        {
          label: "操作",
          width: "60%",
          prop: "opention",
        },
      ],
    };
  },
  computed: {},

  mounted() {},

  methods: {
    onSOSO() {},
    
  
    clickRow(scope) {
      // this.$router.path('/index/reportdateil');
       this.$router.push({name:'reportdateil',params:{id:'123'}});
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