<template>
  <div class="content">
        <Row class="top_banner"> 
            <Col span="8" class="title-style">
                用户管理
            </Col>
            <Col span="14" class="fr">
                <Col span="5">
                    <Select v-model="chosenUserType" @on-change="changeUserFn()"> 
                        <Option v-for="item in selUserList" :value="item.value" :key="item.value">{{ item.label }}</Option>
                    </Select>
                </Col>
                <Col span="6" class="mL10 mR5">
                    <Input v-model="selectUserVal" clearable placeholder="请输入查询值">
                        <span slot="prepend">查询值</span>
                    </Input>
                </Col>
                <Col span="12">
                    <Button shape="circle" icon="ios-search" @click="userSearch" class="mL10 mR5"></Button>
                    <Button shape="circle" icon="md-close" class="mR5"></Button>
                    <Button shape="circle" icon="ios-add" @click="userAdd" class="mR5"></Button>
                    <Button shape="circle" icon="ios-cloud-upload-outline" class="mR5"></Button>
                    <Button shape="circle" icon="ios-cloud-download-outline"></Button>
                </Col>
            </Col>
          </Row>
          <div class="shadow_table">
            <Tabs type="card">
                <TabPane 
                  v-for="(tab, index) in tabList" 
                  :key="index" 
                  :label="tab.label" 
                  :name="tab.name">
                </TabPane>
            </Tabs>
            <Table :columns="userColumns" :data="userData" class="table">
                <template slot-scope="{ row, index }" slot="userAction">
                    <Button type="text" size="small" style="margin-right: 5px" @click="userView(row, index)">查看</Button>
                    <Button type="text" size="small" style="margin-right: 5px" @click="userEdit(row, index)">编辑</Button>
                    <Button type="text" size="small" style="margin-right: 5px" @click="userRemove(row, index)">删除</Button>
                    <Button type="text" size="small" @click="resetPass(row, index)">重置密码</Button>
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
    <!--dialog start-->
  <Modal ref="userModal" 
    v-model="userDialog" 
    width="826"
    :title="userTitle" 
    :loading=true 
    footer-hide
    :mask-closable="false"
    @on-visible-change="closeUserDialog">
        <Form ref="userForm" :model="userForm" :rules="userRule" :label-width="80" inline>
            <FormItem label="用户名" prop="name">
                <Input type="text" v-model="userForm.username" disabled></Input>
            </FormItem>
            <FormItem label="电话" prop="phone">
                <Input type="text" v-model="userForm.phone" :disabled="isUserDisable"></Input>
            </FormItem>
            <FormItem label="姓名" prop="name">
                <Input type="text" v-model="userForm.name" :disabled="isUserDisable"></Input>
            </FormItem>
            <FormItem label="是否启用" prop="isenableBtn">
                <i-switch v-model="userForm.isenableBtn" @on-change="changeIsEnable"></i-switch>
            </FormItem>
        </Form>
        <div class="user_dialog_ft">
            <Button type="primary" @click="userFormOk('userForm')">确定</Button>
        </div>
    </Modal>
  <!--dialog end-->
  </div>
</template>

<script>
export default {
  name: 'user',
  components: {},
  data () {
    return {
      tabList: [
        {
            label: '养老机构信息员',
            name: '养老机构信息员'
        },
        {
            label: '民政干部',
            name: '民政干部'
        },
        {
            label: '系统管理员',
            name: '系统管理员'
        },
        {
            label: '普通管理员',
            name: '普通管理员'
        },
        {
            label: '统计员',
            name: '统计员'
        },
        {
            label: '小程序用户',
            name: '小程序用户'
        }
      ],
      selectUserVal: '',
      chosenUserType: '',
      selUserList:[
        {
            label:'用户名',
            value: '1'
        },
        {
            label:'姓名',
            value:'2'
        },
        {
            label:'手机',
            value: '3'
        }
      ],
      userTitle:'',
      userForm: {
          username: '',
          phone: '',
          name: '',
          isenableBtn: false
      },  
      userRule: {
        username: [
            { required: true, message: '用户名不能为空', trigger: 'blur' }
        ],
        phone: [
            { required: true, message: '电话不能为空', trigger: 'blur' }
        ],
        name: [
            { required: true, message: '姓名不能为空', trigger: 'blur' }
        ]
      },
      isUserDisable: false,
      userTableChoose: '',
      userTableItem: '',
      userColumns: [
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
        // {
        //   title: '用户属性',
        //   key: 'userAttr',
        //   width: 100
        // },  
        {
          title: '用户名',
          key: 'username',
          width: 80
        },
        {
          title: '姓名',
          key: 'name',
          width: 80
        },
        {
          title: '最后登录时间',
          key: 'lastdate',
          width: 150
        },
        {
          title: '手机',
          key: 'phone',
          width: 120
        },
        {
          title: '是否启用',
          key: 'isenable',
          width: 90
        },
        {
          title: '有效时间',
          key: 'effectivetime',
          width: 100
        },
        {
          title: '操作',
          key: 'action',
          slot: 'userAction',
          width: 260,
          align: 'center'
        }
      ],
      userData: [
        {
          id: '1',
          userAttr: '养老机构信息员',  
          username: 'JIADAN',
          name: '贾丹',
          lastdate: '2020/7/29 13:42',
          phone: '15901011533',
          isenable: '1',
          effectivetime: '2020/7/29'
        },
        {
          id: '2',
          userAttr: '民政干部',  
          username: 'CHUAN',
          name: '王思川',
          lastdate: '2020/7/29 13:42',
          phone: '15901011533',
          isenable: '0',
          effectivetime: '2020/7/29'
        }
      ],
      userPage:{
          index: 1,
          size: 10,
          total: 0
      },
      userDialog: false,
      changeUserType: '1',
    }
  },
  created(){
      for(let item of this.userData){
          item.isenable = item.isenable === '1' ? '已启用' : '未启用'
      }
  },
  methods: {  
    changeUserFn(){
        console.log(this.changeUserType);
    },  
    userSearch(){
        
    },
    changeIsEnable (status) {
        this.userForm.isenableBtn = status;
    },
    userAdd(){
        this.userTitle = '新增用户';
        this.userForm =  {
          username: '',
          phone: '',
          name: '',
          isenable: false
        };
        this.isUserDisable = false;
        this.userDialog = true;
    },
    userView(row){
        this.userTitle = '查看用户';
        this.userForm = row;
        this.isUserDisable = true;
        this.userDialog = true;
    },
    userEdit(row){
        this.userTitle = '编辑用户';
        this.userForm = row;
        this.isUserDisable = false;
        this.userDialog = true;
    },
    userRemove(row, index){
        if(this.userTableChoose === ''){
            this.$Message.warning('请先选择一条数据，再操作!');
            return;
        }
        if(this.userTableChoose !== row.id){
            this.$Message.warning('请选择相对应的数据!');
            return;
        }
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
    },
    resetPass(row, index){
        if(this.userTableChoose === ''){
            this.$Message.warning('请先选择一条数据，再操作!');
            return;
        }
        if(this.userTableChoose !== row.id){
            this.$Message.warning('请选择相对应的数据!');
            return;
        }
        this.$Modal.confirm({
          title: '提示',
          content: '<p>确定要重置这条数据吗？</p>',
          onOk: () => {
              this.$Message.success('重置成功!');
          },
          onCancel: () => {
              console.log('取消重置');
          }
      });
    },
    userFormOk(name){
      this.$refs[name].validate((valid) => {
          if (valid) {
              this.$refs[name].resetFields();
              this.$Message.success('成功!');
          } else {
              this.$Message.error('失败!');
          }
      })
    },
    closeUserDialog(e){
      if(e === false){
          this.userDialog = false;
      };
    },
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
  }
}
</script>
<style lang="less" scoped>
@import "~@/assets/variables.less";
.title-style {
  font-size: 20px;
  font-family: Helvetica Neue, Helvetica Neue-Bold;
  font-weight: 700;
  text-align: left;
  color: #000000;
  padding-left: 20px;
}
.user_dialog_ft{
    width:100%;
    margin: 0 auto;
    text-align: center;
}
.top_banner /deep/ .ivu-card-extra{
    width: 540px;
    top: 5px;
    right: 0;
}
.shadow_table {
  width: 1300px;
  padding: 10px;
  margin-left: 20px;
  margin-top: 10px;
  background: @Cffffff;
  border-radius: 10px;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);
}

@media (max-width: 1400px) {
  .shadow_table {
    width: calc(~"var(--ratio) * 1300px");
  }
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
.page_style{
  width:100%;
  margin: 20px auto; 
  text-align: center; 
  overflow: hidden;
}
.fr{
    float: right;
}
</style>
