<template>
  <div>
      <el-form :inline="true" class="demo-form-inline">
          <el-form-item>
            <el-input
              v-model="serviceCode"
              class="search_name"
              size="mini"
              placeholder="输入服务号">
            </el-input>
          </el-form-item>
          <el-form-item>
            <el-button
              type="text"
              @click="onSearch()"
              class="el-icon-search">查询
            </el-button>
          </el-form-item>
          <el-form-item>
            <el-button
              class="el-icon-refresh"
              type="text"
              @click="refreshData">刷新
            </el-button>
          </el-form-item>
          <!--
          <el-form-item>
            <el-button
              class="el-icon-circle-plus-outline"
              type="text"
              @click="dialogVisible = true">添加
            </el-button>
          </el-form-item>
          -->
      </el-form>
      <el-table
        :data="tableData"
        highlight-current-row
        border
        style="width: 100%">
        <el-table-column
          label="ID">
          <template slot-scope="scope">
            <span>{{ scope.row.id }}</span>
          </template>
        </el-table-column>
        <el-table-column
          label="大类">
          <template slot-scope="scope">

            <span>{{ scope.row.bigCategory }}</span>
          </template>
        </el-table-column>
        <!--
        <el-table-column
          label="姓名">
          <template slot-scope="scope">
            <el-popover trigger="hover" placement="right">
              <p>姓名: {{ scope.row.userName }}</p>
              <p>住址: {{ scope.row.userAddress }}</p>
              <p>日期：{{ scope.row.userDate }}</p>
              <div slot="reference" class="name-wrapper">
                <el-button type="text">{{ scope.row.userName }}</el-button>
              </div>
            </el-popover>
          </template>
        </el-table-column>
        -->
        <el-table-column
          label="子类">
          <template slot-scope="scope">
            <span>{{ scope.row.subCategory }}</span>
          </template>
        </el-table-column>

        <el-table-column
          label="服务码">
          <template slot-scope="scope">
            <span>{{ scope.row.svcCode }}</span>
          </template>
        </el-table-column>

        <el-table-column
          label="服务名称">
          <template slot-scope="scope">
            <span>{{ scope.row.svcName }}</span>
          </template>
        </el-table-column>

        <el-table-column
          label="场景码">
          <template slot-scope="scope">
            <span>{{ scope.row.sceneCode }}</span>
          </template>
        </el-table-column>

        <el-table-column
          label="场景名称">
          <template slot-scope="scope">
            <span>{{ scope.row.sceneName }}</span>
          </template>
        </el-table-column>

        <el-table-column
          label="交易码">
          <template slot-scope="scope">
            <span>{{ scope.row.tradeCode }}</span>
          </template>
        </el-table-column>

        <el-table-column
          label="交易名称">
          <template slot-scope="scope">
            <span>{{ scope.row.tradeName }}</span>
          </template>
        </el-table-column>

        <el-table-column
          label="服务调用方">
          <template slot-scope="scope">
            <span>{{ scope.row.consumer }}</span>
          </template>
        </el-table-column>

        <el-table-column
          label="服务提供方">
          <template slot-scope="scope">
            <span>{{ scope.row.provider }}</span>
          </template>
        </el-table-column>

        <el-table-column
          label="服务状态">
          <template slot-scope="scope">
            <span>{{ scope.row.status }}</span>
          </template>
        </el-table-column>

        <el-table-column
          label="备注">
          <template slot-scope="scope">
            <span>{{ scope.row.remarks }}</span>
          </template>
        </el-table-column>

<!--
        <el-table-column
          label="操作"
          fixed="right"
          width="100">
          <template slot-scope="scope">
            <el-button
              size="mini"
              icon="el-icon-edit"
              @click="handleEdit(scope.$index, scope.row)">编辑
            </el-button>
            <el-button
              size="mini"
              type="danger"
              icon="el-icon-delete"
              @click="handleDelete(scope.$index, scope.row)">删除
            </el-button>
          </template>
        </el-table-column>

        -->
      </el-table>
<!--
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="70px" class="demo-ruleForm" size="medium">
        <el-dialog
          title="添加"
          :append-to-body='true'
          :visible.sync="dialogVisible"
          width="80%"
          :before-close="handleClose">
          <el-input type="hidden" v-model="ruleForm.userId"/>
          <el-form-item label="时间" prop="userDate">
            <el-date-picker type="datetime" placeholder="选择日期" v-model="ruleForm.userDate" style="width: 100%;"></el-date-picker>
          </el-form-item>
          <el-form-item label="姓名" prop="userName">
            <el-input v-model="ruleForm.userName"></el-input>
          </el-form-item>
          <el-form-item label="住址" prop="userAddress">
            <el-input v-model="ruleForm.userAddress"></el-input>
          </el-form-item>

          <span slot="footer" class="dialog-footer">
            <el-button @click="cancel()" size="medium">取 消</el-button>
            <el-button @click="addUser()" type="primary" size="medium">确 定</el-button>
          </span>
        </el-dialog>
      </el-form>
-->
<!--
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="70px" class="demo-ruleForm" size="medium">
      <el-dialog
        title="编辑"
        :append-to-body='true'
        :visible.sync="dialogUpdate"
        width="80%"
        :before-close="handleClose">
        <el-input type="hidden" v-model="ruleForm.userId"/>
        <el-form-item label="时间" prop="userDate">
          <el-date-picker type="datetime" placeholder="选择日期" v-model="ruleForm.userDate" style="width: 100%;"></el-date-picker>
        </el-form-item>
        <el-form-item label="姓名" prop="userName">
          <el-input v-model="ruleForm.userName"></el-input>
        </el-form-item>
        <el-form-item label="住址" prop="userAddress">
          <el-input v-model="ruleForm.userAddress"></el-input>
        </el-form-item>

        <span slot="footer" class="dialog-footer">
            <el-button @click="cancel()" size="medium">取 消</el-button>
            <el-button @click="updateUser()" type="primary" size="medium">确 定</el-button>
          </span>
      </el-dialog>
    </el-form>
    -->
      <br>
      <div class="pages">
        <el-pagination
          background
          :disabled = "disablePage"
          :current-page.sync="currentPage"
          small
          layout="prev, pager, next"
          :page-size="pageSize"
          :total="total"
          @current-change="handleCurrentChange">
        </el-pagination>
      </div>
  </div>
</template>

<script>
    export default {
        data() {
            return {
                ruleForm: {
                    userId: '',
                    userName: '',
                    userDate: '',
                    userAddress: ''
                },
                rules: {
                    userName: [
                        { required: true, message: '请输入姓名', trigger: 'blur' },
                        { min: 2, max: 7, message: '长度在 2 到 7 个字符', trigger: 'blur' }
                    ],
                    userAddress: [
                        { required: true, message: '请输入住址', trigger: 'blur' },
                        { min: 5, message: '长度大于 5 个字符', trigger: 'blur' }
                    ],
                },
                tableData: [],
                serviceCode: '',
                provider:'',
                dialogVisible: false,
                dialogUpdate: false,
                pageSize: 50,
                currentPage: 1,
                total: 0,
                disablePage: false
            }
        },
        methods: {
            handleEdit(index, row) {
                this.dialogUpdate = true;
                this.ruleForm = Object.assign({}, row); //这句是关键！！！
            },
            handleDelete(index, row) {
                console.log(index, row);
                this.$confirm('删除操作, 是否继续?', '提示', {
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning'
                }).then(() => {
                    let postData = this.qs.stringify({
                        userId: row.userId,
                    });
                    this.axios({
                        method: 'post',
                        url:'/delete',
                        data:postData
                    }).then(response =>
                    {
                        this.getPages();
                        this.currentPage = 1;
                        this.axios.post('http://localhost:9090/overview/list').then(response =>
                        {
                          console.log('开始请求')
                            this.tableData = response.data;
                        }).catch(error =>
                        {
                            console.log(error);
                        });
                        this.$message({
                            type: 'success',
                            message: '删除成功!'
                        });
                        console.log(response);
                    }).catch(error =>
                    {
                        console.log(error);
                    });

                }).catch(() => {
                    this.$message({
                        type: 'info',
                        message: '已取消删除'
                    });
                });
            },
            handleClose(done) {
                this.$confirm('确认关闭？')
                    .then(_ => {
                        done();
                    })
                    .catch(_ => {});
            },
            handleCurrentChange() {
                console.log(`当前页: ${this.currentPage}`);
                let postData = this.qs.stringify({
                    page: this.currentPage
                });
                this.axios({
                    method: 'post',
                    url:'http://localhost:9090/overview/list',
                    data:postData
                }).then(response =>
                {
                    console.log("post data ,"+postData)
                    this.tableData = response.data;
                }).catch(error =>
                {
                    console.log(error);
                });
            },
            cancel() {
                this.dialogUpdate = false;
                this.dialogVisible = false;
                this.emptyUserData();
            },
            emptyUserData(){
                this.ruleForm = {
                    userName: '',
                    userDate: '',
                    userAddress: ''
                }
            },
            addUser() {
                let postData = this.qs.stringify({
                    userDate: this.ruleForm.userDate,
                    userName: this.ruleForm.userName,
                    userAddress: this.ruleForm.userAddress
                });
                this.axios({
                    method: 'post',
                    url:'/insert',
                    data:postData
                }).then(response =>
                {
                    this.axios.post('/page').then(response =>
                    {
                        this.tableData = response.data;
                        this.currentPage = 1;
                        this.$message({
                            type: 'success',
                            message: '已添加!'
                        });
                    }).catch(error =>
                    {
                        console.log(error);
                    });
                    this.getPages();
                    this.dialogVisible = false
                    console.log(response);
                }).catch(error =>
                {
                    console.log(error);
                });
            },
            updateUser() {
                let postData = this.qs.stringify({
                    userId: this.ruleForm.userId,
                    userDate: this.ruleForm.userDate,
                    userName: this.ruleForm.userName,
                    userAddress: this.ruleForm.userAddress
                });
                this.axios({
                    method: 'post',
                    url:'/update',
                    data:postData
                }).then(response =>
                {
                    this.handleCurrentChange();
                    this.cancel();
                    this.$message({
                        type: 'success',
                        message: '更新成功!'
                    });
                    console.log(response);
                }).catch(error =>
                {
                    this.$message({
                        type: 'success',
                        message: '更新失败!'
                    });
                    console.log(error);
                });
            },
            onSearch() {
                let postData = this.qs.stringify({
                    serviceCode: this.serviceCode
                });
                this.axios({
                    method: 'post',
                    url: 'http://localhost:9090/overview/listBySvcCode',
                    data: postData
                }).then(response =>
                {
                  console.log('on search')
                    this.tableData = response.data;
                    this.disablePage = true;
                }).catch(error =>
                {
                    console.log(error);
                });
            },
            getPages() {
                this.axios.post('/rows').then(response =>
                {
                  console.log('get pages')
                    this.total = response.data;
                }).catch(error =>
                {
                    console.log(error);
                });
            },
            refreshData() {
                location.reload();
            }
        },
        created() {
            /*this.axios.get('static/user.json').then(response =>
            {
                this.tableData = response.data.tableData;
                this.total = response.data.tableData.length;
                // console.log(JSON.parse(JSON.stringify(response.data))['tableData'])
            });*/
            this.axios.post('http://localhost:9090/overview/list').then(response =>
            {
              console.log("created list")
                this.tableData = response.data;
            }).catch(error =>
            {
              console.log("created,error")
                console.log(error);
            });

            this.axios.post('http://localhost:9090/overview/rows').then(response =>
            {
                console.log('created get rows'+ response.data)
                this.total = response.data;
            }).catch(error =>
            {
                console.log(error);
            });

        },
    }
</script>
<style scoped>
  .search_name{
    width: 200px;
  }
  .pages{
    margin: 0px;
    padding: 0px;
    text-align: right;
  }
</style>
