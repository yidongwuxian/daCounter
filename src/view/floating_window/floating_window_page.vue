<template>
  <div class="floating_window_page content">
    <!-- <div>漂浮窗与轮播图</div> -->
    <Row class="top_banner">
      <Col span="8" class="title-style"> 历史记录 </Col>
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
          style="
            vertical-align: top;
            margin-right: 15px;
            background: #000;
            color: #fff;
          "
          @click="goto('drafts')"
          >草稿箱</Button
        >
        <span @click="edit()">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            width="33"
            height="33"
            viewBox="0 0 33 33"
          >
            <image
              id="修改_列表_"
              data-name="修改（列表）"
              width="33"
              height="33"
              xlink:href="data:image/png;base64,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"
            />
          </svg>
        </span>
        <span>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="33"
            height="33"
            viewBox="0 0 33 33"
          >
            <g id="组_27" data-name="组 27" transform="translate(-1667 -264)">
              <circle
                id="椭圆_33"
                data-name="椭圆 33"
                cx="16.5"
                cy="16.5"
                r="16.5"
                transform="translate(1667 264)"
              />
              <g
                id="组_11"
                data-name="组 11"
                transform="translate(290.69 -53.5)"
                style="isolation: isolate"
              >
                <line
                  id="直线_22"
                  data-name="直线 22"
                  x2="11"
                  y2="11"
                  transform="translate(1387.5 328.5)"
                  fill="none"
                  stroke="#fff"
                  stroke-linecap="round"
                  stroke-width="2"
                />
                <line
                  id="直线_23"
                  data-name="直线 23"
                  y1="11"
                  x2="11"
                  transform="translate(1387.5 328.5)"
                  fill="none"
                  stroke="#fff"
                  stroke-linecap="round"
                  stroke-width="2"
                />
              </g>
            </g>
          </svg>
        </span>

        <span @click="goto('add')">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="33"
            height="33"
            viewBox="0 0 33 33"
          >
            <g
              id="组_1665"
              data-name="组 1665"
              transform="translate(-975.736 -1372.423) rotate(45)"
            >
              <circle
                id="椭圆_33"
                data-name="椭圆 33"
                cx="16.5"
                cy="16.5"
                r="16.5"
                transform="translate(1667 264)"
              />
              <g
                id="组_11"
                data-name="组 11"
                transform="translate(290.69 -53.5)"
                style="isolation: isolate"
              >
                <line
                  id="直线_22"
                  data-name="直线 22"
                  x2="11"
                  y2="11"
                  transform="translate(1387.5 328.5)"
                  fill="none"
                  stroke="#fff"
                  stroke-linecap="round"
                  stroke-width="2"
                />
                <line
                  id="直线_23"
                  data-name="直线 23"
                  y1="11"
                  x2="11"
                  transform="translate(1387.5 328.5)"
                  fill="none"
                  stroke="#fff"
                  stroke-linecap="round"
                  stroke-width="2"
                />
              </g>
            </g>
          </svg>
        </span>
        <span>
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="33"
            height="33"
            viewBox="0 0 33 33"
          >
            <g id="组_30" data-name="组 30" transform="translate(-1814 -264)">
              <circle
                id="椭圆_34"
                data-name="椭圆 34"
                cx="16.5"
                cy="16.5"
                r="16.5"
                transform="translate(1814 264)"
              />
              <g
                id="组_24"
                data-name="组 24"
                transform="translate(163.618 6.849)"
              >
                <g
                  id="Group_Copy_6"
                  data-name="Group Copy 6"
                  transform="translate(1670.851 275.628) rotate(180)"
                >
                  <path
                    id="Path_3"
                    data-name="Path 3"
                    d="M0,9.628V0L3.851,3.864"
                    transform="translate(3.851 0)"
                    fill="none"
                    stroke="#fff"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-miterlimit="10"
                    stroke-width="2"
                  />
                  <path
                    id="Path_3-2"
                    data-name="Path 3"
                    d="M0,3.851,3.851,0Z"
                    transform="translate(0 0)"
                    fill="none"
                    stroke="#fff"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-miterlimit="10"
                    stroke-width="2"
                  />
                </g>
                <path
                  id="路径_1"
                  data-name="路径 1"
                  d="M5691.891,1559.5v5.737h13.217V1559.5"
                  transform="translate(-4031.391 -1286.519)"
                  fill="none"
                  stroke="#fff"
                  stroke-linecap="round"
                  stroke-width="2"
                />
              </g>
            </g>
          </svg>
        </span>

      </Col>
    </Row>

    <div class="shadow_table">
      <Table ref="modalTable" :columns="modalColumns" :data="data1"></Table>
      <Page
        style="text-align: center"
        :total="logPage.total"
        :current="logPage.index"
        :page-size="logPage.size"
        size="small"
        prev-text="上一页"
        next-text="下一页"
        show-total
        @on-change="changeLogPage"
        @on-page-size-change="changeLogSize"
      >
      </Page>
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
        {
          title: ' ',
          key: 'id',
          width: 70,
          align: 'center',
          render: (h, params) => {
            // console.log(h,params)
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
                  'on-change': (value) => {
                    self.currentChoose = id
                    self.currentItem = params.row
                    // console.log(self.currentItem)
                  }
                }
              })
            ])
          }
        },
        { type: 'index', width: 60, align: 'center', title: '序号' },
        { title: '标题', key: 'name' },
        { title: '创建人', key: 'age' },
        { title: '主题', key: 'age' },
        { title: '创建时间', key: 'date' }
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
      ],
      logPage: {
        index: 1,
        size: 10,
        total: 0
      }
    }
  },
  methods: {
    goto (str) {
      if (str === 'add') {
        this.$router.push('floating_window_add_page')
      } else if (str === 'drafts') {
        this.$router.push('floating_window_drafts_page')
      }
    },
    edit () {
      // this.$refs.selection
      console.log(this.$refs.modalTable)
    },
    changeLogPage (i) {
      // i是分页中当前页的页码
      this.logPage.index = i
      this.userQuery()
    },
    changeLogSize (s) {
      // s为页面大小
      this.logPage.index = 1
      this.logPage.size = s
      this.userQuery()
    }
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
