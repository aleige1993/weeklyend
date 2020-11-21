<template>
  <div class="waige">
    <el-row>
      <el-col>
        <div class="rightflex marigbot">
          <div>
            <el-button type="primary" @click="adduser()" size="small"
              ><i class="el-icon-plus"></i> 新增员工</el-button
            >
          </div>
          <div>
            <el-input
            style="width: 200px"
            size="small"
            placeholder="输入手机号查询"
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

    <el-dialog :title="isAdd?'新增员工信息':'修改员工信息'" :visible.sync="drawer">
      <el-form
        :model="ruleForm"
        :rules="rules"
        ref="ruleForm"
        label-width="100px"
        size="small"
        class="demo-ruleForm"
      > 
        <el-row>
          <el-col :span="11">
            <el-form-item label="姓名" prop="name">
              <el-input v-model="ruleForm.name"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="11">
            <el-form-item label="手机号码" prop="mobile">
              <el-input v-model="ruleForm.mobile"></el-input>
            </el-form-item>
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="11">
            <el-form-item label="部门" prop="department">
              <el-select v-model="ruleForm.department" placeholder="请选择部门">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
          </el-col>
          <el-col :span="11">
            <el-form-item label="结构部门" prop="structure">
              <el-select v-model="ruleForm.structure" placeholder="请选择结构部门">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
          </el-col>
        </el-row> 
         <el-row>
          <el-col :span="11">
            <el-form-item label="角色职位" prop="role">
              <el-input v-model="ruleForm.role"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="11"> 
            <el-form-item :label="isAdd?'创建密码':'修改密码'" prop="paswd">
              <el-input v-model="ruleForm.paswd"></el-input>
            </el-form-item> 
          </el-col>
        </el-row>
        <el-row>
          <el-col :span="11">
            <el-form-item label="是否可查阅" prop="ischeck">
               <el-radio-group v-model="ruleForm.ischeck">
            <el-radio label="是"></el-radio>
            <el-radio label="否"></el-radio>
          </el-radio-group>
            </el-form-item>
          </el-col>
          <el-col :span="11">
           <el-form-item label="是否可批复" prop="isreply">
          <el-radio-group v-model="ruleForm.isreply">
            <el-radio label="是"></el-radio>
            <el-radio label="否"></el-radio>
          </el-radio-group>
        </el-form-item>
          </el-col>
        </el-row> 
        <el-row> 
          <el-col :span="11">
           <el-form-item label="是否领导" prop="isleader">
          <el-radio-group v-model="ruleForm.isleader">
            <el-radio label="是"></el-radio>
            <el-radio label="否"></el-radio>
          </el-radio-group>
        </el-form-item>
          </el-col>
        </el-row> 
       <div class="modebitsubt">
          <el-button   @click="resetForm('ruleForm')">重置</el-button>
          <el-button   type="primary" @click="submitForm('ruleForm')"
            >提交</el-button
          >
       </div>
      </el-form>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: "userInfo",
  props: [""],
  data() {
    return {
      isAdd:true,
      ruleForm: {
        name: "",
        mobile: "",
        department: "",
        structure: "",
        role: '',
        isleader: '',
        ischeck: '',
        isreply:'',
        paswd:''
      },
      rules: {
        name: [
          { required: true, message: "请输入姓名", trigger: "blur" }, 
        ],
         mobile: [
          { required: true, message: "请输入手机号码", trigger: "blur" }, 
        ],
        paswd: [
          { required: true, message: "请设置密码", trigger: "blur" }, 
        ],
         department: [
          { required: true, message: "请选择部门", trigger: 'change' }, 
        ],
         structure: [
          { required: true, message: "请选择部门结构", trigger: 'change' }, 
        ],
         role: [
          { required: true, message: "请输入职位", trigger: "blur" }, 
        ],
         isleader: [
          { required: true, message: "请选择是否领导", trigger: 'change' }, 
        ],
         ischeck: [
          { required: true, message: "请选择是否可以查阅", trigger: 'change' }, 
        ],
         isreply: [
          { required: true, message: "请选择是否可以批复", trigger: 'change'}, 
        ],
      },
      drawer: false,
      tableData: [
        {
          shouji: "1231231231",
        },
      ],
      columnData: [
        {
          label: "姓名",
          prop: "shouji",
          width: "40%",
        },
        {
          label: "手机号码",
          prop: "shouji",
          width: "40%",
        },
        {
          label: "部门",
          prop: "shouji",
          width: "60%",
        },
        {
          label: "结构部门",
          prop: "shouji",
          width: "60%",
        },
        {
          label: "角色职位",
          prop: "shouji",
          width: "60%",
        },
        {
          label: "是否领导",
          prop: "shouji",
          width: "30%",
        },
        {
          label: "是否可以查阅下级周报",
          prop: "shouji",
          width: "30%",
        },
        {
          label: "是否可以批复下级周报",
          prop: "shouji",
          width: "30%",
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