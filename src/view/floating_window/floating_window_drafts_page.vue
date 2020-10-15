<template>
  <div class="floating_window_page content">
    <!-- <div>漂浮窗与轮播图</div> -->
    <!-- <Row class="top_banner">
      <Col span="8" class="title-style">
        历史记录
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
      <Col span="6">
        <Button
          style="vertical-align:top; margin-right: 15px;background:#000;color:#fff"
          >草稿箱</Button
        >
        <div class="icon_div icon_edit" @click="edit()"></div>
        <div class="icon_div icon_add" @click="goto('add')"></div>
      </Col>
    </Row> -->

    <div class="shadow_table">
      <Table ref="modalTable" :columns="modalColumns" :data="data1">
        <template slot-scope="{ row, index }" slot="action">
          <Button
            type="primary"
            size="small"
            style="margin-right: 5px"
            @click="edit(index)"
            >编辑</Button
          >
          <Button type="error" size="small" @click="remove(index)">删除</Button>
        </template>
      </Table>
    </div>
  </div>
</template>

<script>
export default {
  name: 'floatingWindow_page',
  components: {},
  data () {
    return {
      value2: ['2016-01-01', '2016-02-15'],

      currentChoose: '',
      currentItem: '',
      modalColumns: [
        // {
        //   title: " ",
        //   key: "id",
        //   width: 70,
        //   align: "center",
        //   render: (h, params) => {
        //     // console.log(h,params)
        //     let id = params.row.id;
        //     let flag = false;
        //     if (this.currentChoose === id) {
        //       flag = true;
        //     } else {
        //       flag = false;
        //     }
        //     let self = this;
        //     return h("div", [
        //       h("Radio", {
        //         props: {
        //           value: flag
        //         },
        //         on: {
        //           "on-change": value => {
        //             self.currentChoose = id;
        //             self.currentItem = params.row;
        //             // console.log(self.currentItem)
        //           }
        //         }
        //       })
        //     ]);
        //   }
        // },
        { type: 'index', width: 60, align: 'center', title: '序号' },
        { title: '标题', key: 'name' },
        { title: '创建人', key: 'age' },
        { title: '主题', key: 'age' },
        { title: '创建时间', key: 'date' },
        {
          title: '操作',
          slot: 'action',
          width: 150,
          align: 'center'
        }
      ],

      data1: [
        {
          id: '1',
          name: 'John Brown',
          age: 18,
          address: 'New York No. 1 Lake Park',
          date: '2016-10-03'
        },
        {
          id: '2',
          name: 'Jim Green',
          age: 24,
          address: 'London No. 1 Lake Park',
          date: '2016-10-01'
        },
        {
          id: '3',
          name: 'Joe Black',
          age: 30,
          address: 'Sydney No. 1 Lake Park',
          date: '2016-10-02'
        }
      ]
    }
  },
  methods: {
    goto (str) {
      if (str === 'add') {
        this.$router.push('floating_window_add_page')
      }
    },
    edit () {
      // this.$refs.selection
      console.log(this.$refs.modalTable)
    },
    remove () {}
  }
}
// import "@/assets/variables.less"
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
.top_banner {
  margin-top: 20px;
}
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
  margin-right: 15px;
  // margin-left:10px;
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
  height: 665px;
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
    height: calc(~"var(--ratio) * 665px");
  }
}
</style>
