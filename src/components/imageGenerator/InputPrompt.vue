<template  >
  <div>
  <el-tooltip class="box-item" effect="dark" content="说出你想要画的内容，说的越详细图画越近似，可以通过拆成多个描述词以逗号分割进行描述" placement="top-start">
        <span class="demonstration" style="line-height:  30pt;">希望出现的内容</span>
  </el-tooltip>
    <div>
  <!-- <el-tooltip class="box-item" effect="dark" content="随机从aitag.top抽取抽签魔导师魔法" placement="top-start">
    <el-switch v-model="randomPrompt" class="ml-2" inline-prompt size="large"
               style="--el-switch-on-color:  #17c8cb; --el-switch-off-color:#13ce66" active-text="随机抽签" inactive-text="手动输入"
               @change="switchRandomPrompt" />
  </el-tooltip> -->
    </div>

  <div class="slider-demo-block" style="margin-top:10px;">
    <el-input v-show="promptIsShow" :autosize="{ minRows: 4, maxRows: 10 }" v-model="prompt" maxlength="1000"
              @change="promptChange" placeholder="描述希望图片出现的内容，可以多个词用逗号分隔（中国龙，金色），或一个完整句子（一条金色的中国龙）"
              show-word-limit type="textarea"  />
  </div>
  <el-tooltip class="box-item" effect="dark" content="如果图片中出现不想要的内容，在此指出哪里有问题，比如手有问题说手坏了，人物没有头发，说没有头发" placement="top-start">
    <span class="demonstration" style="line-height: 30pt;">不希望出现的内容</span>
  </el-tooltip>
  <div class="slider-demo-block">
    <el-input :autosize="{ minRows: 2, maxRows: 6 }" v-model="negative_prompt" maxlength="1500"
              placeholder="描述图片中不希望出现的内容，可以多个词用逗号分隔（手坏了，低质量），或一个完整句子（低质量的图片）" show-word-limit type="textarea" @click.native="dialogVisible = false"/>
  </div>
  <el-dialog class="dialogxx" :visible.sync="dialogVisible" append-to-body title="输入图像中希望出现的词">
    输入图片中希望出现的内容，如果不清楚可以查询<a href="https://aibooru.online" target="_blank">aibooru.online</a>&nbsp;&nbsp;
    <a href="https://aitag.top" target="_blank">aitag.top</a> &nbsp;&nbsp;
    <a href="https://wolfchen.top/tag/" target="_blank">wolfchen tag</a>&nbsp;&nbsp; ，或者开启随机抽签随机抽一组词
    <el-tooltip class="box-item" effect="dark" content="随机从aitag.top抽取抽签魔导师魔法" placement="top-start">
      <el-switch v-model="randomPrompt" class="ml-2" inline-prompt size="large"
                 style="--el-switch-on-color:  #ff4949; --el-switch-off-color:#13ce66" active-text="随机抽签"
                 inactive-text="手动输入" @change="switchRandomPrompt" />
    </el-tooltip>
    <p>如果需要lora，可以使用 &lt;lora:名称:1&gt;</p>
    <el-input class="inputcss" v-model="prompt" type="textarea" :autosize="{ minRows: 4, maxRows: 10 }" maxlength="1000"
              @change="promptChange" show-word-limit></el-input>
  </el-dialog>
  </div>
</template>
<style>
.dialogxx {
  border-radius: 18px !important;
}

.inputcss {
  font-size: large;
}
</style>
<script >



const DEFAULT_NAGATIVE_PROMPT = ""


export default {
  data() {
    return {
      prompt: '',
      promptDialogTxt: '',
      negative_prompt: DEFAULT_NAGATIVE_PROMPT,
      randomPrompt: false,
      promptIsShow: true,
      dialogVisible: false
    }
  },
  created() {
    this.$bus1.$on('getPromptInfo', (callback) => {
      callback(this.prompt, this.negative_prompt, this.randomPrompt)
    });

    this.$bus1.$on('setRandomPrompt', (data) => {
      this.randomPrompt = data.randomPrompt
    })
    this.$bus1.$on('setPromptInfo', (data) => {
      this.prompt = data.prompt
      if (this.negative_prompt == "") {
        this.negative_prompt = data.negativePrompt
      }
    });
  },
  methods: {
    switchRandomPrompt(b) {
      if (b) {
        this.dialogVisible = false
        this.$bus1.$emit("showRandomTagDialog", {})
      }
    },
    promptChange() {
      this.randomPrompt = false
    }
  }
}
</script>