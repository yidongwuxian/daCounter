<template>
  <div class="content">
    <Row class="top_banner">
      <Col span="8">
        <span class="title-style">角色管理</span>
        <span style="float:right">
          <Input placeholder="Enter text" style="width: auto">
            <Icon type="ios-search" slot="suffix" />
          </Input>
        </span>
      </Col>

      <Col span="16">
        <div>
          <span class="title-style">菜单信息</span>
          <span style="float:right">         <span>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="33"
            height="33"
            viewBox="0 0 33 33"
          >
            <g id="组_54" data-name="组 54" transform="translate(-1788 -184)">
              <circle
                id="椭圆_32"
                data-name="椭圆 32"
                cx="16.5"
                cy="16.5"
                r="16.5"
                transform="translate(1788 184)"
              />
              <g
                id="组_31"
                data-name="组 31"
                transform="translate(785.075 -78.12)"
              >
                <path
                  id="路径_27"
                  data-name="路径 27"
                  d="M3000.251,4183.717h14.739l3.375,3.666v12.822h-18.114Z"
                  transform="translate(-1989.549 -3913)"
                  fill="none"
                  stroke="#fff"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                />
                <path
                  id="路径_28"
                  data-name="路径 28"
                  d="M3006.146,4183.717v5.381h6.2v-5.381"
                  transform="translate(-1990.27 -3913)"
                  fill="none"
                  stroke="#fff"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                />
                <g
                  id="矩形_32"
                  data-name="矩形 32"
                  transform="translate(1013.925 278.12)"
                  fill="#fff"
                  stroke="#fff"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                >
                  <rect width="11" height="9" stroke="none" />
                  <rect x="1" y="1" width="9" height="7" fill="none" />
                </g>
              </g>
            </g>
          </svg>
        </span></span>
        </div>
      </Col>
    </Row>

    <Row>
      <Col span="8">
        <div class="shadow_left">
          <Table ref="modalTable" :columns="modalColumns" :data="data1"></Table>
        </div>
      </Col>
      <Col span="16">
        <div class="shadow_right">
          <Tree :data="data2" show-checkbox></Tree>
        </div>
      </Col>
    </Row>
    <!-- <Modal
      ref="userModal"
      v-model="userDialog"
      width="826"
      :title="userTitle"
      :loading="true"
      footer-hide
      :mask-closable="false"
      @on-visible-change="closeUserDialog"
    >
      <Form
        ref="userForm"
        :model="userForm"
        :rules="userRule"
        :label-width="80"
        inline
      >
        <FormItem label="用户名" prop="name">
          <Input type="text" v-model="userForm.username" disabled></Input>
        </FormItem>
        <FormItem label="电话" prop="phone">
          <Input
            type="text"
            v-model="userForm.phone"
            :disabled="isUserDisable"
          ></Input>
        </FormItem>
        <FormItem label="姓名" prop="name">
          <Input
            type="text"
            v-model="userForm.name"
            :disabled="isUserDisable"
          ></Input>
        </FormItem>
        <FormItem label="是否启用" prop="isenableBtn">
          <i-switch
            v-model="userForm.isenableBtn"
            @on-change="changeIsEnable"
          ></i-switch>
        </FormItem>
      </Form>
      <div class="user_dialog_ft">
        <Button type="primary" @click="userFormOk('userForm')">确定</Button>
      </div>
    </Modal> -->
    <!--dialog end-->
  </div>
</template>

<script>
export default {
  name: "user",
  components: {},
  data() {
    return {
      currentChoose: "",
      currentItem: "",
      modalColumns: [
        {
          title: " ",
          key: "id",
          width: 60,
          align: "center",
          render: (h, params) => {
            let id = params.row.id;
            let flag = false;
            if (this.currentChoose === id) {
              flag = true;
            } else {
              flag = false;
            }
            let self = this;
            return h("div", [
              h("Radio", {
                props: {
                  value: flag,
                },
                on: {
                  "on-change": (value) => {
                    self.currentChoose = id;
                    self.currentItem = params.row;
                    // console.log(self.currentItem)
                  },
                },
              }),
            ]);
          },
        },
        { title: "角色", key: "name", align: "center" },
      ],
      data1: [
        {
          id: "1",
          name: "John Brown",
        },
        {
          id: "2",
          name: "Jim Green",
        },
        {
          id: "3",
          name: "Joe Black",
        },
      ],

      data2: [
        {
          title: "parent 1",
          expand: true,
          children: [
            {
              title: "parent 1-1",
              expand: true,
              children: [
                {
                  title: "leaf 1-1-1",
                },
                {
                  title: "leaf 1-1-2",
                },
              ],
            },
            {
              title: "parent 1-2",
              expand: true,
              children: [
                {
                  title: "leaf 1-2-1",
                },
                {
                  title: "leaf 1-2-1",
                },
              ],
            },
          ],
        },
      ],

      // tabList: [
      //   {
      //     label: "养老机构信息员",
      //     name: "养老机构信息员",
      //   },
      //   {
      //     label: "民政干部",
      //     name: "民政干部",
      //   },
      //   {
      //     label: "系统管理员",
      //     name: "系统管理员",
      //   },
      //   {
      //     label: "普通管理员",
      //     name: "普通管理员",
      //   },
      //   {
      //     label: "统计员",
      //     name: "统计员",
      //   },
      //   {
      //     label: "小程序用户",
      //     name: "小程序用户",
      //   },
      // ],
      // selectUserVal: "",
      // chosenUserType: "",
      // selUserList: [
      //   {
      //     label: "用户名",
      //     value: "1",
      //   },
      //   {
      //     label: "姓名",
      //     value: "2",
      //   },
      //   {
      //     label: "手机",
      //     value: "3",
      //   },
      // ],
      // userTitle: "",
      // userForm: {
      //   username: "",
      //   phone: "",
      //   name: "",
      //   isenableBtn: false,
      // },
      // userRule: {
      //   username: [
      //     {
      //       required: true,
      //       message: "用户名不能为空",
      //       trigger: "blur",
      //     },
      //   ],
      //   phone: [
      //     {
      //       required: true,
      //       message: "电话不能为空",
      //       trigger: "blur",
      //     },
      //   ],
      //   name: [
      //     {
      //       required: true,
      //       message: "姓名不能为空",
      //       trigger: "blur",
      //     },
      //   ],
      // },
      // isUserDisable: false,
      // userTableChoose: "",
      // userTableItem: "",
      // userColumns: [
      //   {
      //     title: " ",
      //     key: "id",
      //     width: 70,
      //     align: "center",
      //     render: (h, params) => {
      //       let id = params.row.id;
      //       let flag = false;
      //       if (this.userTableChoose === id) {
      //         flag = true;
      //       } else {
      //         flag = false;
      //       }
      //       let self = this;
      //       return h("div", [
      //         h("Radio", {
      //           props: {
      //             value: flag,
      //           },
      //           on: {
      //             "on-change": (value) => {
      //               self.userTableChoose = id;
      //               self.userTableItem = params.row;
      //             },
      //           },
      //         }),
      //       ]);
      //     },
      //   },
      //   // {
      //   //   title: '用户属性',
      //   //   key: 'userAttr',
      //   //   width: 100
      //   // },
      //   {
      //     title: "用户名",
      //     key: "username",
      //     width: 80,
      //   },
      //   {
      //     title: "姓名",
      //     key: "name",
      //     width: 80,
      //   },
      //   {
      //     title: "最后登录时间",
      //     key: "lastdate",
      //     width: 150,
      //   },
      //   {
      //     title: "手机",
      //     key: "phone",
      //     width: 120,
      //   },
      //   {
      //     title: "是否启用",
      //     key: "isenable",
      //     width: 90,
      //   },
      //   {
      //     title: "有效时间",
      //     key: "effectivetime",
      //     width: 100,
      //   },
      //   {
      //     title: "操作",
      //     key: "action",
      //     slot: "userAction",
      //     width: 260,
      //     align: "center",
      //   },
      // ],
      // userData: [
      //   {
      //     id: "1",
      //     userAttr: "养老机构信息员",
      //     username: "JIADAN",
      //     name: "贾丹",
      //     lastdate: "2020/7/29 13:42",
      //     phone: "15901011533",
      //     isenable: "1",
      //     effectivetime: "2020/7/29",
      //   },
      //   {
      //     id: "2",
      //     userAttr: "民政干部",
      //     username: "CHUAN",
      //     name: "王思川",
      //     lastdate: "2020/7/29 13:42",
      //     phone: "15901011533",
      //     isenable: "0",
      //     effectivetime: "2020/7/29",
      //   },
      // ],
      // userPage: {
      //   index: 1,
      //   size: 10,
      //   total: 0,
      // },
      // userDialog: false,
      // changeUserType: "1",
    };
  },
  created() {},
  methods: {},
};
</script>
<style lang="less" scoped>
@import "~@/assets/variables.less";


.title-style {
  height:32px;
  line-height:32px;
  // font-size: 20px;
  // font-family: Helvetica Neue, Helvetica Neue-Bold;
  // font-weight: 700;
  text-align: left;
  color: #000000;
  padding-left: 20px;
}
.user_dialog_ft {
  width: 100%;
  margin: 0 auto;
  text-align: center;
}
.top_banner /deep/ .ivu-card-extra {
  width: 540px;
  top: 5px;
  right: 0;
}

.shadow_left {
  // width: 440px;
  padding: 10px;
  margin-left: 20px;
  margin-top: 10px;
  background: @Cffffff;
  border-radius: 10px;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);
}
.shadow_right {
  // width: 440px;
  padding: 10px;
  margin-left: 20px;
  margin-top: 10px;
  background: @Cffffff;
  border-radius: 10px;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);
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
  .shadow_left {
    // width: calc(~"var(--ratio) * 440px");
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
.page_style {
  width: 100%;
  margin: 20px auto;
  text-align: center;
  overflow: hidden;
}
.fr {
  float: right;
}
</style>
