<template>
  <div class="content">
      <Row class="top_banner"> 
          <Col span="10" class="title-style">
            系统日志
          </Col>
          <Col span="10">
            操作日期
            <DatePicker
              :value="value2"
              format="yyyy/MM/dd"
              type="daterange"
              placement="bottom-end"
              placeholder="Select date"
              style=""
              class="datePicker"
            ></DatePicker>
          </Col>
          <Col span="4">
              <Button shape="circle" icon="ios-search" @click="userSearch" class="mR5"></Button>
              <Button shape="circle" icon="ios-cloud-download-outline"></Button>
          </Col>    
      </Row>
      <div class="shadow_table">
          <Table :columns="logColumns" :data="logData" class="table"></Table>
          <div class="page_style">
              <Page :total="logPage.total"
                  :current="logPage.index"
                  :page-size="logPage.size"
                  size="small"
                  prev-text="上一页"
                  next-text="下一页"
                  show-total
                  @on-change="changeLogPage"
                  @on-page-size-change="changeLogSize">
              </Page>
          </div>
      </div>    
  </div>
</template>

<script>
export default {
  name: 'log',
  components: {},
  data () {
    return {
      value2: ['2016-01-01', '2016-02-15'],
      logTableChoose: '',
      logTableItem: '',
      logColumns: [
        {
          title: ' ',
          key: 'id',
          width: 70,
          align: 'center',
          render: (h, params) => {
            let id = params.row.id
            let flag = false
            if (this.logTableChoose === id) {
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
                    self.logTableChoose = id
                    self.logTableItem = params.row
                  }
                }
              })
            ])
          }
        },
        {
          title: '序号',
          type: 'index',
          width: 60,
          align: 'center'
        },
        {
          title: '操作时间',
          key: 'opertime'
        },  
        // {
        //   title: '用户名',
        //   key: 'username'
        // },
        // {
        //   title: '姓名',
        //   key: 'name'
        // },
        {
          title: 'IP地址',
          key: 'ipaddr',
          width: 150
        },
        {
          title: '操作内容',
          key: 'opercontent'
        },
        {
          title: '用户代理',
          key: 'useragent',
          width: 230
        }
      ],
      logData: [
        {
          id: '1',
          opertime: '2020/7/29',  
          username: 'JIADAN',
          name: '贾丹',
          ipaddr: '192.57.166.95',
          opercontent: '登录',
          useragent: 'MOZILLA/5.0(WINDOWS NT 10.0)'
        },
        {
          id: '2',
          opertime: '2020/7/30',  
          username: 'CHUAN',
          name: '王思川',
          ipaddr: '172.57.166.95',
          opercontent: '修改密码',
          useragent: 'MOZILLA/5.0(WINDOWS NT 10.0)'
        }
      ],
      logPage:{
          index: 1,
          size: 10,
          total: 0
      }
    }
  },
  methods: {    
    userSearch(){
        
    },
      // logPage start
    userQuery: function () {
        var _this = this;
        axios.get(_this.baseUrl + 'queryUser', {
            params: {
                // 向后端传递当前页面、页面大小两个参数
                pageIndex: _this.logPage.index,
                pageSize: _this.logPage.size
            }
        })
            .then(function (response) {
                // 接收查询结果
                _this.logData = response.data.users.list;
                // 改变total所有记录的值
                _this.logPage.total = response.data.users.total;
            })
            .catch(function (err) {
                console.log(err);
            })
    },
    changeLogPage(i) {
        // i是分页中当前页的页码
        this.logPage.index = i;
        this.userQuery();
    },
    changeLogSize(s){
        // s为页面大小
        this.logPage.index = 1;
        this.logPage.size = s;
        this.userQuery();
    },
    // logPage end
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
.datePicker {
  width: 300px;
}
.datePicker /deep/ input {
  text-align: center;
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
.page_style{
  width:100%;
  margin: 20px auto; 
  text-align: center; 
  overflow: hidden;
}
</style>
