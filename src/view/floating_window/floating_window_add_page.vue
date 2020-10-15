<template>
  <div class="floating_window_add_page content">
    <Row class="top_banner">
      <Col span="8" class="title-style">
        历史记录
      </Col>
      <Col span="10">&nbsp;</Col>
      <Col span="6">
        <Button
          style="vertical-align:top; margin-right: 15px;background:#000;color:#fff"
          >发布</Button
        >
        <Button
          style="vertical-align:top; margin-right: 15px;background:#000;color:#fff"
          >存为草稿</Button
        >
      </Col>
    </Row>
    <div class="shadow_table">
      <div>
        <Form ref="form" :model="formItem" :label-width="80">
          <Row>
            <Col span="12">
              <FormItem label="标题">
                <Input
                  v-model="formItem.input"
                  placeholder="Enter something..."
                ></Input> </FormItem
            ></Col>
            <Col span="12">
              <FormItem label="发布区域">
                <Select v-model="formItem.select">
                  <Option value="beijing">New York</Option>
                  <Option value="shanghai">London</Option>
                  <Option value="shenzhen">Sydney</Option>
                </Select>
              </FormItem></Col
            >
          </Row>

          <Row>
            <Col span="12">
              <FormItem label="发布区域">
                <Row>
                  <Col span="20">
                    <Input
                      v-model="formItem.input"
                      placeholder="Enter something..."
                    >
                    </Input>
                  </Col>
                  <Col span="4">
                    <Upload style="width:100%;">
                      <Button style="width:100%;">上传</Button>
                    </Upload>
                  </Col>
                </Row>
              </FormItem>
            </Col>

            <Col span="12">
              <FormItem label="转载出处">
                <Input
                  v-model="formItem.input"
                  placeholder="Enter something..."
                ></Input> </FormItem
            ></Col>
          </Row>

          <Row>
            <Col span="12">
              <FormItem label="作者">
                <Input
                  v-model="formItem.input"
                  placeholder="Enter something..."
                ></Input> </FormItem
            ></Col>
            <Col span="12">
              <FormItem label="原始链接">
                <Input
                  v-model="formItem.input"
                  placeholder="Enter something..."
                ></Input> </FormItem
            ></Col>
          </Row>

          <Row>
            <Col span="12">
              <FormItem label="作者">
                <Select v-model="formItem.select">
                  <Option value="beijing">New York</Option>
                  <Option value="shanghai">London</Option>
                  <Option value="shenzhen">Sydney</Option>
                </Select>
              </FormItem></Col
            >
            <Col span="12">
              <FormItem label="原始链接">
                <DatePicker
                  type="datetime"
                  format="yyyy-MM-dd HH:mm"
                  placeholder="Select date and time(Excluding seconds)"
                  style="width: 100%"
                ></DatePicker> </FormItem
            ></Col>
          </Row>
        </Form>
      </div>
      <div>
        <div ref="editor" style="text-align:left"></div>
      </div>
    </div>
  </div>
</template>

<script>
import E from 'wangeditor'
export default {
  components: {},
  data () {
    return {
      editor: {},
      formItem: {
        input: '',
        select: '',
        radio: 'male',
        checkbox: [],
        switch: true,
        date: '',
        time: '',
        slider: [20, 50],
        textarea: ''
      }
    }
  },
  methods: {},
  mounted () {
    if (this.$route.query.id) {
      this.state = 1
      this.getData()
    }

    this.editor = new E(this.$refs.editor)
    this.editor.customConfig.onchange = html => {
      this.form.content = html
    }
    this.editor.customConfig.debug = true
    this.editor.customConfig.menus = [
      'head', // 标题
      'bold', // 粗体
      'foreColor', // 文字颜色
      'fontSize', // 字号
      'fontName', // 字体
      'italic', // 斜体
      'underline', // 下划线
      'strikeThrough', // 删除线
      // 'backColor',  // 背景颜色
      'link', // 插入链接
      'list', // 列表
      'justify', // 对齐方式
      'quote', // 引用
      // "emoticon", // 表情
      'image', // 插入图片
      // 'table',  // 表格
      // "video" // 插入视频
      // 'code',  // 插入代码
      'undo', // 撤销
      'redo' // 重复
    ]
    // 过滤粘贴过来的文本样式
    this.editor.customConfig.pasteFilterStyle = true
    // 忽略粘贴内容中的图片
    this.editor.customConfig.pasteIgnoreImg = false
    // 上传图片的配置
    this.editor.customConfig.uploadFileName = 'multipartFile' // 设置文件上传的参数名称
    this.editor.customConfig.uploadImgServer =
      '/organization/fileOperation/putObjectByRichText?type=1' // 设置上传文件的服务器路径
    this.editor.customConfig.uploadImgMaxSize = 3 * 1024 * 1024 // 将图片大小限制为 3M

    // let token = getLocalStorage('userToken')
    // this.editor.customConfig.uploadImgHeaders = {
    //   userToken: getLocalStorage("userToken"),
    // };
    // 自定义上传图片事件
    this.editor.customConfig.uploadImgHooks = {
      before: function (xhr, editor, files) {},
      success: function (xhr, editor, result) {
        console.log(xhr)
        console.log(editor)
        console.log(result)
        console.log('上传成功')
      },
      fail: function (xhr, editor, result) {
        console.log(xhr)
        console.log(editor)
        console.log(result)
        console.log('上传失败')
      },
      error: function (xhr, editor) {
        console.log('上传出错')
      },
      timeout: function (xhr, editor) {
        console.log('上传超时')
      }
    }

    this.editor.create()
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

.shadow_table {
  width: 1300px;
  height: 836px;
  padding: 10px;
  margin-left: 20px;
  margin-top: 10px;
  background: @Cffffff;
  border-radius: 10px;
  box-shadow: 0px 2px 14px 0px rgba(0, 0, 0, 0.11);
}

.content /deep/ .ivu-upload {
  width: 100%;
}
.content /deep/ .ivu-select-dropdown {
  z-index: 20000;
}

@media (max-width: 1400px) {
  .shadow_table {
    width: calc(~"var(--ratio) * 1300px");
    height: calc(~"var(--ratio) * 836px");
  }
}
</style>
