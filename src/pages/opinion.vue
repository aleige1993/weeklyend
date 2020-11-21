<template>
  <div class="waige">
    <el-row>
      <el-col>
        <div class="rightflex marigbot">
          <div>
            <el-button type="primary" @click="adduser()" size="small"
              ><i class="el-icon-download"></i>导出意见</el-button
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
               
            <el-table-column
              v-for="(item, index) in columnData"
              :key="index"
              :prop="item.prop"
              :label="item.label"
              :min-width="item.width"
            >
              <template slot-scope="scope">
                <div v-if="item.prop == 'opention'">
                 <el-switch
                    v-model="value1"
                    active-text="显示"
                    inactive-text="隐藏">
                    </el-switch>
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
  name: "opinion",
  props: [""],
  data() {
    return {
      value1:true, 
      isAdd:true,
      drawer: true,
      tableData: [
        {
          title: "1231231231",
          username: "1231231231",
          bumen: "1231231231",
          dianhua: "1231231231",
          datatime: "1231231231", 
          centes: "1231231231", 
        },
      ],
      columnData: [
        {
          label: "标题",
          prop: "title",
          width: "50%",
        },
        {
          label: "发表人",
          prop: "username",
          width: "30%",
        },
        {
          label: "所属部门",
          prop: "bumen",
          width: "40%",
        },
        {
          label: "电话",
          prop: "dianhua",
          width: "30%",
        },
         {
          label: "发表时间",
          prop: "datatime",
          width: "30%",
        },
         {
          label: "意见内容",
          prop: "centes",
        },
        {
          label: "操作",
         width: "40%",
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