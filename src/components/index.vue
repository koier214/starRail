<script setup>
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
  { name: '瓦尔特', desc: '瓦尔特是星穹铁道的守护者之一，拥有强大的力量和智慧。' },
  { name: '布洛妮娅', desc: '布洛妮娅是星穹铁道的指挥官，擅长战术和战略规划。' },
  { name: '希儿', desc: '希儿是星穹铁道的科学家，致力于研究和开发新技术。' },
  { name: '杰帕德', desc: '杰帕德是星穹铁道的工程师，负责维护和修理铁路设施。' },
  { name: '丹恒', desc: '丹恒是星穹铁道的探险家，勇敢无畏，探索未知领域。' },
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
        <el-tag 
          v-for="(item, index) in nameArr" 
          :key="index"
          :type="activeTagIndex === index ? 'success' : 'primary'"
          @click="handleTagClick(index)"
          class="name-tag"
        >
          <h2>{{ item.name }}</h2>
          <h3>{{ item.desc }}</h3>
        </el-tag>
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
  gap: 12px;
  justify-content: center;
}

.name-tag {
  cursor: pointer;
  transition: all 0.3s;
  padding: 12px;
  &:hover {
    transform: scale(1.05);
  }
  
  h2 {
    margin: 0 0 4px 0;
    font-size: 18px;
  }
  
  h3 {
    margin: 0;
    font-size: 14px;
    font-weight: normal;
  }
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