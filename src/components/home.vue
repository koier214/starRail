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
  { name: '阿兰', desc: '为了保护大家而受伤，本来就是一件值得自豪的事。' },
  { name: '银枝', desc: '我谨在此，以一朵玫瑰的沉重份量，向你致意。' },
  { name: '真理医生', desc: '我甚至无法向一个蠢材解释何为[蠢材]。' },
  { name: '波提欧', desc: '这么说吧，我的联觉信标被改造过。反正他宝贝的你们现在只能听到我和那些欠喵的小可爱这么讲话了...小可爱，小可爱，小可爱!喏，你看。' },
  { name: '星期日', desc: '总有一处乐园需要人来建成。那誓愿有如天上的太阳，也许我在触及它前便会熔毁...但有些苦难是必须要经受的。' },
  { name: '景元', desc: '善弈者无通盘妙手。人们会为一子妙手力挽狂澜而喜，却不为大局危倾而忧。' },
  { name: '彦青', desc: '叫声老师，是敬你有一技之长。接下来，我可不会手下留情了。' },
  { name: '罗刹', desc: '这具棺柩非我之物。在下只是受人所托，将其遗体送回罗浮安置而已。' },
  { name: '丹恒·饮月', desc: '我不是任何人的影子。' },
  { name: '椒丘', desc: '说了很多次啦，这叫医食同源——烹煮即是炼药;炼药即是烹煮。以食疗济愈病患，乃是我的独门绝学。俗话说，不想当医士的厨子当不了好幕僚...' },
  { name: '貘泽', desc: '有的人沉默是无欲望，有的人沉默是没思想，而我只是不想说话。' },
  { name: '瓦尔特', desc: '这片银河容得下任何的可能性，而人的命运也不应当只有上天给予的那一条道路。' },
  { name: '丹恒', desc: '生离死别之事，每分每秒都在宇宙中上演。你我的悲伤是真实的，但也并无特殊之处。' },
  { name: '刃', desc: '死亡何时而至?我等得有些心焦了' },
  { name: '砂金', desc: '你可以随意利用我，也可以在恰当的时机背叛我，利用与背叛都是价值互换的手段。但我从不做赔本实卖，也希望你...不要让我失望。' },
  { name: '米沙', desc: 'XX要努力工作，攒下很多积蓄，以后能像大人们一样在群星之间旅行探索!' },
  { name: '加拉赫', desc: '调饮是一门关乎感性的技术，在梦中调制汽水需加入当下的心情，如果烦闷，就浓郁一点;如果快乐，就甜蜜一些...调制饮料，也是调制人生。' },
  { name: '杰帕德', desc: '忠诚并非天生的美德。被效忠之人也需拥有相应的资格。' },
  { name: '桑博', desc: '在我这儿没有什么生意是不能谈的，只要钱到位。' },
  { name: '卢卡', desc: '偷偷告诉你，冠军的秘诀就是趁着别人休息的时候刻苦训练。' },
  { name: '万敌', desc: '我是悬锋的王储[迈德漠斯],亦是奥赫玛的战士[万敌]。若想了解更多，便观我一战，或与我一战。' },
  { name: '那刻夏', desc: '我名为阿那克萨戈拉斯，神悟树庭七贤人之一，智种学派的创立者。不必我多说了，第一，别叫我那刻夏。第二，别打断我——沉默是金。切记。' },
])

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

// 处理轮播图切换
const handleCarouselChange = (index) => {
  activeIndex.value = index
}

const isShow = (index) => {
  if (activeTagIndex.value === index) {
    return true
  }else {
    return false
  }
}
// 组件挂载时加载保存的数据
onMounted(() => {
  loadSavedData()
})
</script>
<template>
    <div class="container">
      <!-- 滚动图片 -->
      <el-carousel 
        type="card" 
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
  
      <div class="tag-container">
        <div 
          v-for="(item, index) in nameArr" 
          :key="index"
          @click="handleTagClick(index)"
          class="name-tag"
        >
          <el-tag class="name-tag-item">
            <h2 class="name-title">{{ item.name }}</h2>
          </el-tag>
          <div v-if="isShow(index)" class="tag-description">
            <h3>{{ item.desc }}</h3>
          </div>
        </div>
      </div>

      

    </div>
  </template>

<style scoped lang="scss">
.container {
    margin-top: 10px;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 20px;
}

.carousel-image {
    background: rgba(0, 0, 0, 0.5);
    padding-top: 10px;
  width: 80%;
  height: 80%;
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
  gap: 20px;
  justify-content: center;
  background-color: red;
}

.name-tag {
  cursor: pointer;
  transition: all 0.3s;
  padding: 12px;
  width: 80px;
  text-align: center;
  border-radius: 8px;


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
  margin-top: 10px;
  font-size: 14px;
  color: #777;
  font-weight: normal;
  background-color: #fafafa;
  border-radius: 6px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}


.el-carousel__item {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f5f7fa;
}

.cardBox {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;
  
}
</style>