<template>
  <div class="container">
    <div class="overview">
      <img src="https://s21.ax1x.com/2024/03/14/pFg3krQ.png" alt="" />
      <div class="overview-text">
        <p class="item">
          累计收录<span style="color: red">{{ data / 2 }}</span
          >项非遗
        </p>
        <p class="item">
          <span style="color: red">{{ data }}</span
          >件数字藏品
        </p>
      </div>
    </div>
    <hr />
    <div class="content-wrapper">
      <contentCard
        v-for="(item, index) in content"
        :key="index"
        :imageUrl="item.imgUrl"
        :title="item.title"
        :description="item.description"
      ></contentCard>
    </div>
  </div>
</template>

<script>
import contentCard from "./contentCard.vue";

export default {
  name: "GuiZhou",
  data() {
    return {
      content: [
        {
          imgUrl: "https://s21.ax1x.com/2024/03/14/pFg1bvD.png",
          title: "枫香染",
          description:
            "简介：枫香染，作为一种古老的民间手工技艺，它的颜色古朴， 花纹雅致，寓意吉祥，独具风格，被誉为“布依族不需出土的文物”， 印染的成品主要被当地用以裁制床单、被面、头巾、背带等， 其青、蓝、白色的图案蕴蓄着深厚的民族情感与内涵。 2008年被列入第二批国家级非物质文化遗产名录。",
        },
        {
          imgUrl: "https://s21.ax1x.com/2024/03/14/pFg1HgO.png",
          title: "侗绣",
          description:
            "简介：侗绣属于刺绣一种，即侗族刺绣，是侗族人民用一针一线在侗布上刺出来的。侗绣风格独特，自然、朴素、大方，以三龙侗绣为代表，独具民族特色，是侗族人民智慧的结晶，侗族历史文化发展的见证。侗绣的图案内容以花鸟及几何图案为主，有的还绣有人物建筑图案，现代的侗绣还进行一些更大胆的创新，绣有非常时尚的元素。",
        },
        {
          imgUrl: "https://s21.ax1x.com/2024/03/14/pFg178K.png",
          title: "苗族织锦技艺",
          description:
            "简介：苗族织锦技艺，流传于贵州省台江县、凯里市、雷山县的传统手工技艺，国家级非物质文化遗产之一。据《峒溪纤志》记载：“黎人取中国彩帛，拆取色丝和吉贝，织之成锦。”织锦历史最早可追溯至3000年前。20世纪80年代，黔东南地区的乡村苗寨都盛行织锦之风。苗锦是苗族妇女利用当地所产的蚕丝、苎麻、木棉等纤维染彩而织。苗族织锦又称织花，即以编织形成的花纹织物。彩纬充分覆盖在织物表面，正面色彩艳丽。",
        },
      ],
      data: 0,
    };
  },
  components: {
    contentCard,
  },
  mounted() {
    // 获取查询参数
    // const name = this.$route.query.name;
    this.data = this.$route.query.number;
    console.log(this.data);
    // 在这里进行相应的处理
  },
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column; /* 将子元素垂直排列 */
  align-items: center; /* 水平居中 */
  gap: 20px; /* 设置子元素之间的间距 */
}

.overview {
  display: flex; /* 将子元素水平排列 */
  align-items: center; /* 垂直居中 */
  margin-top: 50px;
}

.overview-text {
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif /* 字体 */;
  margin-left: 50px;
}

.overview img {
  margin-left: 20px; /*图片与文字之间的间距 */
}

.overview-text .item {
  margin: 0; /* 移除默认的上下间距 */
  font-size: 26px; /* 字体大小 */
}

.content-wrapper {
  display: flex;
  flex-wrap: wrap;
  justify-content: center; /* 子元素水平居中 */
  gap: 20px;
}
</style>
