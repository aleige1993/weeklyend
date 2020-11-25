<template>
  <div class="waige">
    <el-row>
      <el-col>
        <div class="rightflex marigbot">
          <div>
            <el-button type="primary" @click="adduser()" size="small"
              ><i class="el-icon-plus"></i> 新增角色</el-button
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
                  <el-button
                    @click="clickRow(scope.row)"
                    type="primary"
                    size="small"
                    icon="el-icon-edit"
                    >修改</el-button
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

    <el-dialog width="30%" :title="isAdd?'新增角色':'修改角色'" :visible.sync="drawer">
      <el-form
        :model="ruleForm"
        :rules="rules"
        ref="ruleForm"
        label-width="80px"
        size="small"
        class="demo-ruleForm"
      > 
        <el-row>
            <el-form-item label="角色" prop="name">
              <el-input v-model="ruleForm.name" placeholder="请输入角色职称"></el-input>
            </el-form-item>
        </el-row>
        <el-row>
            <el-form-item label="权限" prop="department">
              <el-checkbox-group v-model="ruleForm.department">
                <el-checkbox label="查阅" name="type"></el-checkbox>
                <el-checkbox label="审批" name="type"></el-checkbox>
              </el-checkbox-group>
            </el-form-item>
            <!-- <el-form-item label="权限" prop="department" >
              <el-select v-model="ruleForm.department" multiple placeholder="请选择权限" >
                <el-option label="查阅" value="shanghai"></el-option>
                <el-option label="审批" value="beijing"></el-option>
              </el-select>
            </el-form-item> -->
        </el-row> 
       <div class="modebitsubt">
          <el-button   @click="resetForm('ruleForm')">取消</el-button>
          <el-button   type="primary" @click="submitForm('ruleForm')"
            >确定</el-button
          >
       </div>
      </el-form>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: "rolepart",
  props: [""],
  data() {
    return {
      isAdd:true,
      ruleForm: {
        name: "",
        department: []
         
      },
      rules: {
        name: [
          { required: true, message: "请输入角色职称", trigger: "blur" }, 
        ],
         department: [
          { required: true, message: "请选择权限", trigger: 'change' }, 
        ]
      },
      drawer: false,
      tableData: [
        {
          shouji: "1231231231",
        },
      ],
      columnData: [
        {
          label: "角色职称",
          prop: "shouji",
          width: "80%",
        },
        {
          label: "权限",
          prop: "shouji",
          width: "80%",
        },
        {
          label: "操作",
          width: "50%",
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
    },
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
  },
};
</script>
<style lang='css' scoped>
.waige {
  padding: 40px;
  width: 80%;
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