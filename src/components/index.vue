<script setup lang="ts">
import { ref, onMounted } from 'vue'
const picture = ref([
  { url: '/assets/starRail/a1.png', name: '' },
  { url: '/assets/starRail/a2.png', name: '' },
  { url: '/assets/starRail/a3.png', name: '' },
  { url: '/assets/starRail/a4.png', name: '' },
  { url: '/assets/starRail/a5.png', name: '' },
  { url: '/assets/starRail/a6.png', name: '' },
  { url: '/assets/starRail/a7.png', name: '' },
  { url: '/assets/starRail/a8.png', name: '' },
  { url: '/assets/starRail/a9.png', name: '' },
  { url: '/assets/starRail/a10.png', name: '' },
  { url: '/assets/starRail/a11.png', name: '' },
  { url: '/assets/starRail/a12.png', name: '' },
  { url: '/assets/starRail/a13.png', name: '' },
  { url: '/assets/starRail/a14.png', name: '' },
  { url: '/assets/starRail/a15.png', name: '' },
  { url: '/assets/starRail/a16.png', name: '' },
  { url: '/assets/starRail/a17.png', name: '' },
  { url: '/assets/starRail/a18.png', name: '' },
  { url: '/assets/starRail/a19.png', name: '' },
  { url: '/assets/starRail/a20.png', name: '' },
  { url: '/assets/starRail/a21.png', name: '' },
  { url: '/assets/starRail/a22.png', name: '' }
]);

const nameArr = ref([
  { name: '阿兰', desc: '为了保护大家而受伤，本来就是一件值得自豪的事。', isShow: false },
  { name: '银枝', desc: '我谨在此，以一朵玫瑰的沉重份量，向你致意。', isShow: false },
  { name: '真理医生', desc: '我甚至无法向一个蠢材解释何为[蠢材]。', isShow: false },
  { name: '波提欧', desc: '这么说吧，我的联觉信标被改造过。反正他宝贝的你们现在只能听到我和那些欠喵的小可爱这么讲话了...小可爱，小可爱，小可爱!喏，你看。', isShow: false },
  { name: '星期日', desc: '总有一处乐园需要人来建成。那誓愿有如天上的太阳，也许我在触及它前便会熔毁...但有些苦难是必须要经受的。', isShow: false },
  { name: '景元', desc: '善弈者无通盘妙手。人们会为一子妙手力挽狂澜而喜，却不为大局危倾而忧。', isShow: false },
  { name: '彦青', desc: '叫声老师，是敬你有一技之长。接下来，我可不会手下留情了。', isShow: false },
  { name: '罗刹', desc: '这具棺柩非我之物。在下只是受人所托，将其遗体送回罗浮安置而已。', isShow: false },
  { name: '丹恒·饮月', desc: '我不是任何人的影子。', isShow: false },
  { name: '椒丘', desc: '说了很多次啦，这叫医食同源——烹煮即是炼药;炼药即是烹煮。以食疗济愈病患，乃是我的独门绝学。俗话说，不想当医士的厨子当不了好幕僚...', isShow: false },
  { name: '貘泽', desc: '有的人沉默是无欲望，有的人沉默是没思想，而我只是不想说话。', isShow: false },
  { name: '瓦尔特', desc: '这片银河容得下任何的可能性，而人的命运也不应当只有上天给予的那一条道路。', isShow: false },
  { name: '丹恒', desc: '生离死别之事，每分每秒都在宇宙中上演。你我的悲伤是真实的，但也并无特殊之处。', isShow: false },
  { name: '刃', desc: '死亡何时而至?我等得有些心焦了', isShow: false },
  { name: '砂金', desc: '你可以随意利用我，也可以在恰当的时机背叛我，利用与背叛都是价值互换的手段。但我从不做赔本实卖，也希望你...不要让我失望。', isShow: false },
  { name: '米沙', desc: 'XX要努力工作，攒下很多积蓄，以后能像大人们一样在群星之间旅行探索!', isShow: false },
  { name: '加拉赫', desc: '调饮是一门关乎感性的技术，在梦中调制汽水需加入当下的心情，如果烦闷，就浓郁一点;如果快乐，就甜蜜一些...调制饮料，也是调制人生。', isShow: false },
  { name: '杰帕德', desc: '忠诚并非天生的美德。被效忠之人也需拥有相应的资格。', isShow: false },
  { name: '桑博', desc: '在我这儿没有什么生意是不能谈的，只要钱到位。', isShow: false },
  { name: '卢卡', desc: '偷偷告诉你，冠军的秘诀就是趁着别人休息的时候刻苦训练。', isShow: false },
  { name: '万敌', desc: '我是悬锋的王储[迈德漠斯],亦是奥赫玛的战士[万敌]。若想了解更多，便观我一战，或与我一战。', isShow: false },
  { name: '那刻夏', desc: '我名为阿那克萨戈拉斯，神悟树庭七贤人之一，智种学派的创立者。不必我多说了，第一，别叫我那刻夏。第二，别打断我——沉默是金。切记。', isShow: false },
])

const handleMore = (index) => {
  nameArr.value[index].isShow = !nameArr.value[index].isShow;
}

// 当前选中的图片索引
const activeIndex = ref(0)
// 当前选中的标签索引
const activeTagIndex = ref(null)

// 从localStorage加载保存的数据
const loadSavedData = () => {
  const savedData = localStorage.getItem('starRailSelections')
  if (savedData) {
    try {
      const parsedData = JSON.parse(savedData)
      picture.value = picture.value.map((item, index) => ({
        ...item,
        name: parsedData[index]?.name || ''
      }))
    } catch (e) {
      console.error('Failed to parse saved data', e)
    }
  }
}

// 保存数据到localStorage
const saveData = () => {
  const dataToSave = picture.value.map(item => ({ 
    url: item.url, 
    name: item.name 
  }))
  localStorage.setItem('starRailSelections', JSON.stringify(dataToSave))
}

// 处理标签点击
const handleTagClick = (tagIndex) => {
  activeTagIndex.value = tagIndex
  // 更新当前显示的图片的名字
  picture.value[activeIndex.value].name = nameArr.value[tagIndex].name
  // 保存更改
  saveData()
}

const handleTagCancel = (tagIndex) => {
  // 清除当前标签的描述
  nameArr.value[tagIndex].desc = ''
  // 清除当前图片的名字
  picture.value[activeIndex.value].name = ''
  // 保存更改
  saveData()
}

// 处理轮播图切换
const handleCarouselChange = (index) => {
  activeIndex.value = index
}
// 组件挂载时加载保存的数据
onMounted(() => {
  loadSavedData()
})
</script>
<template>
    <div class="container">
      <div class="left">
        <div class="tag-container">
          <div 
            v-for="(item, index) in nameArr" 
            :key="index"
            
            class="name-tag"
          >
          <img @click="handleMore(index)" src="../assets/more.png" alt="" width="30" height="30">
            <div class="name-tag-item">
              <h2 class="name-title">{{ item.name }}</h2>
            </div>
            <img @click="handleTagClick(index)" src="../assets/open.png" alt="" width="30" height="30">
            <img @click="handleTagCancel(index)" src="../assets/cancel.png" alt="" width="30" height="30">
            <div v-if="item.isShow" class="tag-description">
              <h3>{{ item.desc }}</h3>
            </div>
          </div>
        </div>
      </div>

      <div class="right">

        <div class="bowen1"></div> 
        <div class="bowen2"></div> 
        <div class="bowen3"></div> 
        <el-carousel 
        height="700px"
        @change="handleCarouselChange"
        :autoplay="false"
        >
          <el-carousel-item v-for="(item, index) in picture" :key="item.url">
            <div class="cardBox">
              <img :src="item.url" :alt="item.name" class="carousel-image">
              <h3 class="image-name">{{ item.name }}</h3>
            </div>
          </el-carousel-item>
        </el-carousel>
        <!-- <el-carousel arrow="always"  @change="handleCarouselChange"   height="700px">
          <el-carousel-item v-for="(item, index) in picture" :key="item.url">
            <div class="cardBox">
              <img :src="item.url" :alt="item.name" class="carousel-image">
              <h3 class="image-name">{{ item.name }}</h3>
            </div>
          </el-carousel-item>
        </el-carousel> -->
      </div>

    </div>
  </template>

<style scoped lang="scss">
.container {
  width: 100vw;    /* 视口宽度 */
  height: 100vh;   /* 视口高度 */
  display: flex;
  justify-content: space-around;
  align-items: center;
  gap: 20px;
  background: linear-gradient(to bottom, rgba(255, 179, 217, 0.8), rgba(0, 183, 204, 0.8));
  overflow: hidden; 

  .left {
    flex: 0 0 450px; /* 固定左侧宽度 */

  }

  .right {
    position: relative;
    width: 60%;
    display: flex;
    justify-content: center;
    align-items: center;
    border-radius: 27.35px;
    background: linear-gradient(to bottom, rgba(255, 179, 217, 0.8), rgba(0, 183, 204, 0.8));
    box-shadow: -27.35px 31.46px 15.04px 0px rgba(0, 0, 0, 0.25),-18.46px 34.19px 22.57px 0px rgba(0, 0, 0, 0.25),-28.72px 73.17px 26.67px 0px rgba(0, 0, 0, 0.25);

    .bowen1 {
      top: 0;
      left: 50px;
      position: absolute;
      height: 200px;
      width: 100px;
      border-radius: 50%;
      border-left: 8px solid #feb8ff;
    }


  }
}

.el-carousel {
  width: 60%;
}

.el-carousel__item {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f5f7fa;
}

.carousel-image {
    background: rgba(0, 0, 0, 0.5);
    padding-top: 10px;
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 8px;
}

.image-name {
    position: absolute;
  color: white;
  font-size: 22px;
  text-align: center;
  background: rgba(0, 0, 0, 0.5);
  padding: 8px 16px;
  border-radius: 20px;
  display: inline-block;
  bottom: 20px;
  left: 0;

}

.tag-container {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
}

.name-tag {
  cursor: pointer;
  transition: all 0.3s;
  padding: 5px;
  width: 200px;
  height: 50px;
  text-align: center;
  border-radius: 8px;
  background: linear-gradient(to bottom, rgba(255, 179, 217, 0.8), rgba(0, 183, 204, 0.8));
  display: flex;
  justify-content: center;
  align-items: center;

}

.name-tag-item {
  padding: 8px 16px;
  font-size: 16px;
  font-weight: bold;
  color: #333;
  position: relative;
}

.name-title {
  margin: 0;
  font-size: 20px;
  color: #3b3b3b;
}

.tag-description {
  z-index: 9999;
  width: 190px;
  position: absolute;
  margin-top: 200px;
  font-size: 14px;
  color: #777;
  font-weight: normal;
  background-color: #fafafa;
  border-radius: 6px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}



.cardBox {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;
  
}

</style>