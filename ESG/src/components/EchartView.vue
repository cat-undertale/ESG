<template>
  <div>
    <el-form :model="dengmiQueryForm" ref="dengmiQueryForm" label-width="100px" class="demo-ruleForm" size="mini">
      <el-row>
        <el-col span="8">
          <el-form-item label="谜面">
            <el-input v-model="dengmiQueryForm.mimian"></el-input>
          </el-form-item>
        </el-col>
        <el-col span="8">
          <el-form-item label="谜目">
            <el-input v-model="dengmiQueryForm.mimu"></el-input>
          </el-form-item>
        </el-col>
        <el-col span="8">
          <el-form-item label="谜格">
            <el-input v-model="dengmiQueryForm.mige"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col span="8">
          <el-form-item label="谜底">
            <el-input v-model="dengmiQueryForm.midi"></el-input>
          </el-form-item>
        </el-col>
        <el-col span="8">
          <el-form-item label="作者">
            <el-input v-model="dengmiQueryForm.zuozhe"></el-input>
          </el-form-item>
        </el-col>
        <el-col span="8">
          <el-form-item label="谜底字数">
            <el-input v-model="dengmiQueryForm.midiLength"></el-input>
          </el-form-item>
        </el-col>
      </el-row>
      <el-row>
        <el-col>
          <el-button type="primary" @click="submitForm" icon="el-icon-search">查询</el-button>
          <el-button type="warning" @click="resetForm" icon="el-icon-search" plain>重置</el-button>
        </el-col>
      </el-row>
    </el-form>
    <el-header></el-header>
    <div v-if="dengmiQueryForm.requestResult">
      <el-table :data="dengmiQueryForm.list.slice((dengmiQueryForm.currentPage-1)*dengmiQueryForm.pagesize,dengmiQueryForm.currentPage*dengmiQueryForm.pagesize)"
                stripe border width="100%" height="350">
        <el-table-column type="index" fixed="left"></el-table-column>
        <el-table-column prop="mimian" label="谜面" width="300" fixed="left">
        </el-table-column>
        <el-table-column prop="dengmiSeq" label="序号">
        </el-table-column>
        <el-table-column prop="mimu" label="谜目">
        </el-table-column>
        <el-table-column prop="mige" label="谜格">
        </el-table-column>
        <el-table-column prop="midi" label="谜底">
        </el-table-column>
        <el-table-column prop="zuozhe" label="作者">
        </el-table-column>
        <el-table-column prop="mizhu" label="注">
        </el-table-column>
        <el-table-column prop="shangxi" label="赏析">
        </el-table-column>
        <el-table-column prop="leixing" label="类型">
        </el-table-column>
        <el-table-column label="操作" fixed="right" width="200px">
          <el-row>
            <el-col :span="10">
              <el-tooltip effect="dark" content="编辑当前行" placement="top">
                <el-button size="mini" @click="dengmiQueryForm.dialogVisible = true">编辑</el-button>
              </el-tooltip>
            </el-col>
            <el-col :span="10">
              <el-tooltip effect="light" content="删除当前行" placement="top">
                <el-button size="mini" @click="dengmiQueryForm.dialogDeleteVisible = true" type="danger" plain>删除</el-button>
              </el-tooltip>
            </el-col>
          </el-row>
        </el-table-column>
        <el-table-column label="操作尝试2">
          <template slot-scope="scope">
            <el-button type="text" @click="checkDetail(scope.row)">查看详情</el-button>
          </template>
        </el-table-column>
      </el-table>
      <div style="margin-top: 5px;"></div>
      <el-pagination
        prev-text="上一页"
        next-text="下一页"
        background
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="dengmiQueryForm.currentPageA"
        :page-sizes="[5,10,50,100]"
        :page-size="5"
        layout="total, sizes, prev, pager, next, jumper"
        :total="dengmiQueryForm.list.length">
      </el-pagination>
    </div>
    <div v-else>
      请求失败！
    </div>
    <el-dialog title="编辑灯谜" :visible.sync="dengmiQueryForm.dialogVisible">
      <el-form :model="modifyForm">
        <el-form-item label="谜面" :label-width="modifyForm.formLabelWidth">
          <el-input v-model="modifyForm.mimian" auto-complete="off"></el-input>
        </el-form-item>
        <el-form-item label="谜目" :label-width="modifyForm.formLabelWidth">
          <el-input v-model="modifyForm.mimu" auto-complete="off"></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dengmiQueryForm.dialogVisible = false">取 消</el-button>
        <el-button type="primary" @click="dengmiQueryForm.dialogVisible = false">确 定</el-button>
      </div>
    </el-dialog>
    <el-dialog title="删除灯谜" :visible.sync="dengmiQueryForm.dialogDeleteVisible">
      <h1><span style="color: red"><strong>确定删除该行数据？删除后不可恢复！</strong></span></h1>
      <el-form>
        <el-form-item label="当前行数据">
          <el-col :span="18">
            <el-input v-model="dengmiQueryForm.deleteShow" readonly></el-input>
          </el-col>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dengmiQueryForm.dialogDeleteVisible = false">取 消</el-button>
        <el-button type="primary" @click="dengmiQueryForm.dialogDeleteVisible = false">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>
<script>
export default {
  name: "dengmiQuery",
  data() {
    return {
      modifyForm:{
        formLabelWidth:'120px',
        mimian:'',
        mimu:''
      },
      dengmiQueryForm: {
        deleteShow:'',
        dialogDeleteVisible:false,
        dialogVisible: false,
        currentRow: null,
        visibleA: false,
        currentPage: 1, //初始页
        pagesize: 5,    //    每页的数据
        currentPageA: 1,
        mimian: '',
        mimu: '',
        mige: '',
        midi: '',
        zuozhe: '',
        midiLength: '',
        list: [],
        requestResult: true,
        thisRowData:{}
      }
    };
  },
  methods: {
    submitForm(formName) {
      console.log(formName.mimu);
      this.$http.get('http://localhost:909/dengmi/showDengmi2').then(function (success) {
        console.log("This request is succeed! Here is the response:");
        this.dengmiQueryForm.list = success.body.result;
        this.dengmiQueryForm.requestResult = true;
      }, function (error) {
        console.log("This request is failed! Here is the response:");
        console.log(error);
        this.dengmiQueryForm.requestResult = false;
      })
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
    handleSizeChange(size) {
      this.dengmiQueryForm.pagesize = size;
      console.log(this.dengmiQueryForm.pagesize)  //每页下拉显示数据
    },
    handleCurrentChange(currentPage) {
      this.dengmiQueryForm.currentPage = currentPage;
      console.log(this.dengmiQueryForm.currentPage)  //点击第几页
    },
    handleEdit(row) {
      this.dengmiQueryForm.deleteShow = row.mimian + "(" + row.mimu + ")" + row.midi + "/" + row.zuozhe;
      // this.dengmiQueryForm.currentRow = row;
      console.log(this.dengmiQueryForm.deleteShow);
      this.modifyForm.mimian=row.mimian;
      this.modifyForm.mimu=row.mimu;

      // console.log("event=" + event);
      // console.log(colunm)
    },
    handleClose(done) {
      this.$confirm('确认关闭？')
        .then(_ => {
          done();
        })
        .catch(_ => {});
    },
    checkDetail(val){
      console.log(val)
    }

  }
}
</script>
<style scoped>
</style>
