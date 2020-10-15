<template>
  <div class="floating_window_page content">
    <div class="shadow_table">
      <Table ref="modalTable" :columns="modalColumns" :data="data1">
        <template slot-scope="{ row, index }" slot="action">
          <Button
            type="primary"
            size="small"
            style="margin-right: 5px"
            @click="edit(index)"
            >下载</Button
          >
          <Button type="error" size="small" @click="remove(index)">删除</Button>
        </template>
      </Table>
      <div style="margin-top:20px;text-align:right">
        <button class="btn" style="margin-right:20px">下载全部安全包</button>
        <button class="btn">删除全部安全包</button>
      </div>
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
        { title: '备份模板', key: 'name' },
        { title: '状态', key: 'age' }, // 已备份，未备份
        { title: '备份时间', key: 'date' },
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

.table {
  border: none;
}
.btn {
  width: 160px;
  height: 37px;
  // font-size: px;
  font-family: PingFang SC, PingFang SC-Medium;
  font-weight: 500;
  text-align: center;
  border-radius: 6px;
  background: #000000;
  color: #ffffff;
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
  .btn{
    width: calc(~"var(--ratio) * 160px");
    height: calc(~"var(--ratio) * 37px");
  }

}
</style>
