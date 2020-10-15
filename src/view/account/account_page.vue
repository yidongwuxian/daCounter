<template>
  <div class="account_page content">
    <div class="shadow">
      <Row style="margin-top:30px">
        <Col span="12">
          <Upload action="//jsonplaceholder.typicode.com/posts/">
            <img
              src="http://118.24.57.72/image/aaa.jpg"
              style="border-radius:50%;width:100px;height:100px;margin-left:50px"
              @click="upload"
            />
            <!-- <Button icon="ios-cloud-upload-outline">Select the file to upload</Button> -->
          </Upload>
        </Col> 
        <Col span="8">&nbsp;</Col>
        <Col span="4">

<svg xmlns="http://www.w3.org/2000/svg" width="87" height="49" viewBox="0 0 87 49">
  <g id="组_19" data-name="组 19" transform="translate(-150 -964)">
    <g id="组_18" data-name="组 18" transform="translate(30)">
      <rect id="矩形_28" data-name="矩形 28" width="87" height="49" rx="24.5" transform="translate(120 964)"/>
    </g>
    <g id="Group_Copy_6" data-name="Group Copy 6" transform="translate(183.588 994.932) rotate(-90)">
      <path id="Path_3" data-name="Path 3" d="M0,20.985V0L8.394,8.422" transform="translate(8.394 0)" fill="none" stroke="#fff" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width="5"/>
      <path id="Path_3-2" data-name="Path 3" d="M0,8.394,8.394,0Z" transform="translate(0 0)" fill="none" stroke="#fff" stroke-linecap="round" stroke-linejoin="round" stroke-miterlimit="10" stroke-width="5"/>
    </g>
  </g>
</svg>



        </Col>
      </Row>
      <Row style="margin-right:40px;margin-top:30px">
        <Form ref="form" :model="formItem" :label-width="80">
          <Row :gutter="32">
            <Col span="12">
              <FormItem label="姓名">
                <Input
                  v-model="formItem.input"
                  placeholder="Enter something..."
                ></Input> </FormItem
            ></Col>
            <Col span="12">
              <FormItem label="电话">
                <Select v-model="formItem.select">
                  <Option value="beijing">New York</Option>
                  <Option value="shanghai">London</Option>
                  <Option value="shenzhen">Sydney</Option>
                </Select>
              </FormItem></Col
            >
          </Row>
        </Form>
      </Row>
      <div style="text-align:center">
        <button class="btn">
          保存
        </button>
      </div>
      <!-- <Row></Row> -->
    </div>
  </div>
</template>

<script>
export default {
  name: '',
  components: {},
  data () {
    return {
      formItem: {}
    }
  },
  methods: {
    upload () {}
  }
}
// import "@/assets/variables.less"
</script>

<style lang="less" scoped>
@import "~@/assets/variables.less";

.shadow {
  width: 1300px;
  height: 836px;
  padding: 10px;
  margin-left: 20px;
  margin-top: 10px;
  background: @Cffffff;
  border-radius: 10px;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);
}
.btn {
  width: 193px;
  height: 48px;
  background: #000000;
  border-radius: 12px;
  color: #fff;
}
@media (max-width: 1400px) {
  .shadow {
    width: calc(~"var(--ratio) * 1300px");
    height: calc(~"var(--ratio) * 665px");
  }
  .btn {
    width: calc(~"var(--ratio) * 193px");
    height: calc(~"var(--ratio) * 48px");
  }
}
</style>
