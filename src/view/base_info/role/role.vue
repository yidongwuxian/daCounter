<template>
  <div class="role_page content">
        <div class="role_box_left">
            <!--role_box_left start-->
            <Row class="mT20">
                <Col span="8">
                    <span class="title-style">角色列表</span>
                </Col>
                <Col span="16" style="float:right;">
                    <Col span="10" class="role_box">
                        <RadioGroup v-model="chosenRoleType" class="role_box_radio" @on-change="changeRoleType()">
                            <Radio v-for="item in radioRoleList" :label="item.label" :key="item.value"></Radio>
                        </RadioGroup>
                    </Col>
                    <Col span="6" class="role_box">
                        <Input search placeholder="请选择" />
                    </Col>
                    <Col>
                        <Button shape="circle" icon="ios-add" class="mL10 mR10" @click="roleAdd"></Button>
                    </Col>
                </Col>
            </Row>
            <div class="shadow_table">
                <Table :columns="roleColumns" :data="roleData" class="table">
                    <template slot-scope="{ row, index }" slot="roleAction">
                        <Button type="text" size="small" style="margin-right: 5px" @click="roleEdit(row, index)">编辑</Button>
                        <Button type="text" size="small" @click="roleRemove(row, index)">删除</Button>
                    </template>
                </Table>
                <div class="page_style">
                    <Page :total="rolePage.total"
                        :current="rolePage.index"
                        :page-size="rolePage.size"
                        size="small"
                        prev-text="上一页"
                        next-text="下一页"
                        show-total
                        @on-change="changeRolePage"
                        @on-page-size-change="changeRoleSize">
                    </Page>
                </div>
            </div>
    </div>
    <!--role_box_left end-->
    <!--role_box_right start-->
    <div class="role_box_right">
        <Row class="mT20">
            <Col span="12" class="title-style">
                用户列表
            </Col>
            <Col span="12" style="float:right;">
                <Col span="16" class="role_box">
                    <Input search placeholder="请输入用户名称" />
                </Col>
                <Col>
                    <Button shape="circle" icon="ios-add" class="mL10 mR10" @click="userAdd"></Button>
                </Col>
            </Col>
        </Row>   
        <div class="shadow_table1">
            <Table :columns="userColumns" :data="userData" class="table">
                <template slot-scope="{ index }" slot="userAction">
                    <Button type="text" size="small" @click="userRemove(index)">删除</Button>
                </template>
            </Table>
            <div class="page_style">
                <Page :total="userPage.total"
                    :current="userPage.index"
                    :page-size="userPage.size"
                    size="small"
                    prev-text="上一页"
                    next-text="下一页"
                    show-total
                    @on-change="changeUserPage"
                    @on-page-size-change="changeUserSize">
                </Page>
            </div>
        </div>
    </div>
  <!--role_box_right end--> 
  <!--dialog start-->
  <Modal ref="roleModal" 
    v-model="roleDialog" 
    :title="roleTitle" 
    :loading=true 
    footer-hide
    :mask-closable="false"
    @on-visible-change="closeRoleDialog">
    <Form ref="roleForm" :model="roleForm" :rules="roleRule" :label-width="80">
          <FormItem label="角色名称" prop="name">
              <Input type="text" v-model="roleForm.name"></Input>
          </FormItem>
          <FormItem label="角色类型" prop="type">
              <Input type="text" v-model="roleForm.type"></Input>
          </FormItem>
          <FormItem label="角色描述" prop="desc">
              <Input type="text" v-model="roleForm.desc"></Input>
          </FormItem>
          <FormItem>
              <Button type="primary" @click="roleFormOk('roleForm')">确定</Button>
          </FormItem>
      </Form>
    </Modal>
  <!--dialog end-->

  <!--dialog start-->
  <Modal ref="userModal" 
    v-model="userDialog" 
    width="826"
    title="选择用户" 
    :loading=true 
    :mask-closable="false"
    @on-visible-change="closeUserDialog">
        <div slot="footer" class="user_dialog_ft">
            <Button type="primary" @click="userDialogOk">确定</Button>
        </div>
        <Row class="mB20">
            <i-col span="8" class="mR10">
                <Input v-model="selectUser.name" clearable placeholder="请输入姓名">
                    <span slot="prepend">姓名</span>
                </Input>
            </i-col>
            <i-col span="8" class="mR10">
                <Input v-model="selectUser.phone" clearable placeholder="请输入手机号">
                    <span slot="prepend">手机号</span>
                </Input>
            </i-col>
            <Button shape="circle" icon="ios-search"></Button>
        </Row>    
        <Table :columns="userTableColumns" :data="userTablegData" class="table"></Table>
        <div style="margin: 10px;overflow: hidden">
            <div style="float: right;">
                <Page :total="userEditPage.total"
                    :current="userEditPage.index"
                    :page-size="userEditPage.size"
                    size="small"
                    prev-text="上一页"
                    next-text="下一页"
                    show-total
                    @on-change="changeUserEditPage"
                    @on-page-size-change="changeUserEditSize">
                </Page>
            </div>
        </div>
    </Modal>
  <!--dialog end-->
  </div>
</template>

<script>
export default {
  name: 'role',
  components: {},
  data () {
    return {
      chosenRoleType: '角色名称',
      radioRoleList: [
        {
            label:'角色名称',
            value:'1'
        },
        {
            label:'角色描述',
            value: '2'
        }
      ],
      currentChoose: '',
      userTableChoose: '',
      roleTitle: '',
      roleDialog: false,
      userDialog: false,
      roleForm: {
        name: '',
        type: '',
        desc: ''
      },
      roleRule: {
        name: [
            { required: true, message: '角色名称不能为空', trigger: 'blur' }
        ]
      },
      selectUser: {
        name: '',
        phone: ''
      }, 
      currentItem: '',
      userTableItem: '',
      roleColumns: [
        {
          title: ' ',
          key: 'id',
          width: 70,
          align: 'center',
          render: (h, params) => {
            let id = params.row.id
            let flag = false
            if (this.currentChoose === id) {
              flag = true
            } else {
              flag = false
            }
            let self = this
            return h('div', [
              h('Radio', {
                props: {
                  value: flag
                },
                on: {
                  'on-change': value => {
                    self.currentChoose = id
                    self.currentItem = params.row
                  }
                }
              })
            ])
          }
        },
        {
          title: '角色名称',
          key: 'name'
        },
        {
          title: '角色类型',
          key: 'type'
        },
        {
          title: '角色描述',
          key: 'desc'
        },
        {
          title: '操作',
          key: 'action',
          slot: 'roleAction',
          width: 150,
          align: 'center'
        }
      ],
      roleData: [
        {
          id: '1',
          name: '系统管理员',
          type: '管理员',
          desc: '管理'
        },
        {
          id: '2',
          name: '普通管理员',
          type: '非管理员',
          desc: '录入'
        },
        {
          id: '3',
          name: '统计员',
          type: '非管理员',
          desc: '测试'
        }
      ],
      userColumns: [
        {
          title: '姓名',
          key: 'name'
        },
        {
          title: '用户名',
          key: 'username'
        },
        {
          title: '操作',
          key: 'action',
          slot: 'userAction',
          width: 150,
          align: 'center'
        }
      ],
      userData: [
        {
          name: '贾丹',
          username: 'JIADAN'
        },
        {
          name: '王思川',
          username: 'CHUAN'
        }
      ],
      userTableColumns: [
        {
          title: ' ',
          key: 'id',
          width: 70,
          align: 'center',
          render: (h, params) => {
            let id = params.row.id
            let flag = false
            if (this.userTableChoose === id) {
              flag = true
            } else {
              flag = false
            }
            let self = this
            return h('div', [
              h('Radio', {
                props: {
                  value: flag
                },
                on: {
                  'on-change': value => {
                    self.userTableChoose = id
                    self.userTableItem = params.row
                  }
                }
              })
            ])
          }
        },
        {
          id: '1',
          title: '用户名',
          key: 'username'
        },
        {
          id: '2',  
          title: '姓名',
          key: 'fullname'
        },
        {
          id: '3',   
          title: '手机号',
          key: 'phone'
        }
      ],
      userTablegData: [
        {
          username: 'JIADAN',
          fullname: '贾丹',
          phone: '15934242342'
        },
        {
          username: 'CHUAN',
          fullname: '王思川',
          phone: '13787242342'
        },
        {
          username: 'ZHANGSAN',
          fullname: '张三',
          phone: '13823423423'
        },
        {
          username: 'LISI',
          fullname: '李四',
          phone: '18787242342'
        }
      ],
      rolePage:{
          index: 1,
          size: 10,
          total: 0
      },
      userPage:{
          index: 1,
          size: 10,
          total: 0
      },
      userEditPage:{
          index: 1,
          size: 10,
          total: 0
      },
    }
  },
  methods: {
    changeRoleType(){
        console.log(this.chosenRoleType);
    },
    roleAdd(){
      this.roleTitle = '新增角色';
      this.roleForm = {
        name: '',
        type: '',
        desc: ''
      };
      this.roleDialog = true;
    },
    roleEdit(row, index){
      this.roleTitle = '编辑角色';
      this.roleForm = row;
      this.roleDialog = true;
    },
    roleRemove (row, index) {
      if(this.currentChoose === ''){
        this.$Message.warning('请先选择一条数据，再操作!');
        return;
      }
      if(this.currentChoose !== row.id){
        this.$Message.warning('请选择相对应的数据!');
        return;
      }
      this.$Modal.confirm({
          title: '提示',
          content: '<p>确定要删除这条数据吗？</p>',
          onOk: () => {
              this.roleData.splice(index, 1);
              this.$Message.success('删除成功!');
          },
          onCancel: () => {
              console.log('取消选择');
          }
      });
    },
    clearRoleForm(){
      if(this.$refs['roleForm']){
        this.$refs['roleForm'].resetFields();
      }
    },
    roleFormOk(name){
      this.$refs[name].validate((valid) => {
          if (valid) {
              this.$Message.success('成功!');
          } else {
              this.$Message.error('失败!');
          }
      })
    },
    closeRoleDialog(e){
      if(e === false){
          this.roleDialog = false;
      };
    },
    closeUserDialog(e){
      if(e === false){
          this.userDialog = false;
      };
    },
    userAdd(){
      this.userDialog = true;
    },
    // rolePage start
    roleQuery: function () {
        var _this = this;
        axios.get(_this.baseUrl + 'queryUser', {
            params: {
                // 向后端传递当前页面、页面大小两个参数
                pageIndex: _this.rolePage.index,
                pageSize: _this.rolePage.size
            }
        })
            .then(function (response) {
                // 接收查询结果
                _this.roleData = response.data.users.list;
                // 改变total所有记录的值
                _this.rolePage.total = response.data.users.total;
            })
            .catch(function (err) {
                console.log(err);
            })
    },
    changeRolePage(i) {
        // i是分页中当前页的页码
        this.rolePage.index = i;
        this.roleQuery();
    },
    changeRoleSize(s){
        // s为页面大小
        this.rolePage.index = 1;
        this.rolePage.size = s;
        this.roleQuery();
    },
    // rolePage end

    // userPage start
    userQuery: function () {
        var _this = this;
        axios.get(_this.baseUrl + 'queryUser', {
            params: {
                // 向后端传递当前页面、页面大小两个参数
                pageIndex: _this.userPage.index,
                pageSize: _this.userPage.size
            }
        })
            .then(function (response) {
                // 接收查询结果
                _this.userData = response.data.users.list;
                // 改变total所有记录的值
                _this.userPage.total = response.data.users.total;
            })
            .catch(function (err) {
                console.log(err);
            })
    },
    changeUserPage(i) {
        // i是分页中当前页的页码
        this.userPage.index = i;
        this.userQuery();
    },
    changeUserSize(s){
        // s为页面大小
        this.userPage.index = 1;
        this.userPage.size = s;
        this.userQuery();
    },
    // userPage end
    
    // userEditPage start
    userEditQuery: function () {
        var _this = this;
        axios.get(_this.baseUrl + 'queryUser', {
            params: {
                // 向后端传递当前页面、页面大小两个参数
                pageIndex: _this.userEditPage.index,
                pageSize: _this.userEditPage.size
            }
        })
            .then(function (response) {
                // 接收查询结果
                _this.userTablegData = response.data.users.list;
                // 改变total所有记录的值
                _this.userEditPage.total = response.data.users.total;
            })
            .catch(function (err) {
                console.log(err);
            })
    },
    changeUserEditPage(i) {
        // i是分页中当前页的页码
        this.userEditPage.index = i;
        this.userEditQuery();
    },
    changeUserEditSize(s){
        // s为页面大小
        this.userEditPage.index = 1;
        this.userEditPage.size = s;
        this.userEditQuery();
    },
    // userEditPage end
    userDialogOk(){
      if(this.userTableChoose === ''){
        this.$Message.warning('请先选择一条数据，再操作!');
        return;
      }
    },
    userRemove (index) {
      this.$Modal.confirm({
          title: '提示',
          content: '<p>确定要删除这条数据吗？</p>',
          onOk: () => {
              this.userData.splice(index, 1);
              this.$Message.success('删除成功!');
          },
          onCancel: () => {
              console.log('取消选择');
          }
      });
    }
  }
}
</script>

<style lang="less" scoped>
@import "~@/assets/variables.less";
.datePicker {
  width: 300px;
}
.datePicker /deep/ input {
  text-align: center;
}

.icon_add {
  background: url("~@/assets/images/add.png");
}
.icon_edit {
  background: url("~@/assets/images/edit.png");
}

.icon_div {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  display: inline-block;
  background-size: 100% 100%;
}

.table {
  border: none;
}

.content /deep/ .ivu-table:after {
  width: 0px;
}
.content /deep/.ivu-table th {
  background-color: @Cffffff;
}
.title-style {
  font-size: 20px;
  font-family: Helvetica Neue, Helvetica Neue-Bold;
  font-weight: 700;
  text-align: left;
  color: #000000;
  padding-left: 20px;
}
.role_page{
    display: flex;
}
.role_box_left{
    width: 650px;
}
.shadow_table {
  width: 760px;
  padding: 10px;
  margin-left: 20px;
  margin-top: 10px;
  background: @Cffffff;
  border-radius: 10px;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);
}

@media (max-width: 1400px) {
  .shadow_table {
    width: calc(~"var(--ratio) * 760px");
  }
}
.role_box_right{
    width: 400px;
}
.shadow_table1 {
  width: 540px;
  padding: 10px;
  margin-left: 20px;
  margin-top: 10px;
  background: @Cffffff;
  border-radius: 10px;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);
}

@media (max-width: 1400px) {
  .shadow_table1 {
    width: calc(~"var(--ratio) * 540px");
  }
}

.role_box /deep/ .ivu-card-extra{
    top:5px !important;
}
.user_dialog_ft{
    width:100%;
    margin: 0 auto;
    text-align: center;
}
.page_style{
  width:100%;
  margin: 20px auto; 
  text-align: center; 
  overflow: hidden;
}
.role_box_radio{
    margin-top: 5px;
}
</style>
