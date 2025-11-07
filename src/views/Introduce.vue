<template>
  <div class="product-browse-container">
    <!-- 轮播图部分 -->
    <div class="swiper-section">
      <el-carousel height="400px" indicator-position="outside">
        <el-carousel-item v-for="item in 5" :key="item">
          <div class="carousel-item">
            <img :src="`https://picsum.photos/1200/400?random=${item}`" alt="轮播图${item}">
            <div class="carousel-text">
              <h3>商品轮播图 {{ item }}</h3>
              <p>展示精美的商品图片</p>
            </div>
          </div>
        </el-carousel-item>
      </el-carousel>
    </div>

    <!-- 商品展示部分 -->
    <div class="products-section">
      <h2 class="section-title">推荐商品</h2>
      <div class="products-grid">
        <div class="product-card" v-for="product in products" :key="product.id">
          <div class="product-image">
            <img :src="product.image" alt="{{ product.name }}">
          </div>
          <div class="product-info">
            <h3 class="product-name">{{ product.name }}</h3>
            <p class="product-description">{{ product.description }}</p>
            <div class="product-footer">
              <span class="product-price">¥{{ product.price.toFixed(2) }}</span>
              <span class="product-promotion">{{ product.promotion }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// 模拟商品数据
const products = ref([
  {
    id: 1,
    name: '智能音箱',
    description: '高品质音效，智能语音助手',
    price: 299.00,
    promotion: '限时优惠',
    image: 'https://picsum.photos/200/200?random=1'
  },
  {
    id: 2,
    name: '无线耳机',
    description: '降噪功能，超长续航',
    price: 399.00,
    promotion: '买一送一',
    image: 'https://picsum.photos/200/200?random=2'
  },
  {
    id: 3,
    name: '智能手机',
    description: '高性能处理器，高清屏幕',
    price: 2999.00,
    promotion: '新品上市',
    image: 'https://picsum.photos/200/200?random=3'
  },
  {
    id: 4,
    name: '平板电脑',
    description: '轻薄便携，高清显示',
    price: 1999.00,
    promotion: '直降200',
    image: 'https://picsum.photos/200/200?random=4'
  },
  {
    id: 5,
    name: '智能手表',
    description: '健康监测，运动追踪',
    price: 1299.00,
    promotion: '满减优惠',
    image: 'https://picsum.photos/200/200?random=5'
  },
  {
    id: 6,
    name: '笔记本电脑',
    description: '轻薄设计，强劲性能',
    price: 5999.00,
    promotion: '学生优惠',
    image: 'https://picsum.photos/200/200?random=6'
  },
  {
    id: 7,
    name: '智能电视',
    description: '4K高清，智能系统',
    price: 3999.00,
    promotion: '限时折扣',
    image: 'https://picsum.photos/200/200?random=7'
  },
  {
    id: 8,
    name: '无线充电器',
    description: '快速充电，智能识别',
    price: 99.00,
    promotion: '买二送一',
    image: 'https://picsum.photos/200/200?random=8'
  },
  {
    id: 9,
    name: '游戏手柄',
    description: '无线连接，舒适握持',
    price: 199.00,
    promotion: '新品特惠',
    image: 'https://picsum.photos/200/200?random=9'
  },
  {
    id: 10,
    name: '智能门锁',
    description: '指纹识别，远程控制',
    price: 899.00,
    promotion: '安全保障',
    image: 'https://picsum.photos/200/200?random=10'
  }
])
</script>

<style scoped>
.product-browse-container {
  width: 100%;
  min-height: 100vh;
  background-color: #f5f5f5;
}

.swiper-section {
  width: 100%;
  margin-bottom: 40px;
}

.carousel-item {
  position: relative;
  width: 100%;
  height: 400px;
  overflow: hidden;
}

.carousel-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.carousel-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: white;
  text-align: center;
  background-color: rgba(0, 0, 0, 0.5);
  padding: 20px;
  border-radius: 8px;
}

.carousel-text h3 {
  font-size: 28px;
  margin-bottom: 10px;
}

.carousel-text p {
  font-size: 16px;
}

.products-section {
  width: 100%;
  padding: 0 20px;
  max-width: 1200px;
  margin: 0 auto;
  margin-bottom: 40px;
}

.section-title {
  font-size: 24px;
  margin-bottom: 20px;
  color: #333;
  text-align: center;
}

.products-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 20px;
  justify-items: center;
}

.product-card {
  width: 100%;
  max-width: 220px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.product-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.15);
}

.product-image {
  width: 100%;
  height: 200px;
  overflow: hidden;
}

.product-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.product-card:hover .product-image img {
  transform: scale(1.05);
}

.product-info {
  padding: 15px;
}

.product-name {
  font-size: 16px;
  font-weight: 600;
  margin-bottom: 8px;
  color: #333;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.product-description {
  font-size: 14px;
  color: #666;
  margin-bottom: 12px;
  line-height: 1.4;
  height: 40px;
  overflow: hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}

.product-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.product-price {
  font-size: 18px;
  font-weight: 700;
  color: #e60012;
}

.product-promotion {
  font-size: 12px;
  color: white;
  background-color: #ff6b6b;
  padding: 3px 8px;
  border-radius: 4px;
}

@media (max-width: 768px) {
  .products-grid {
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
  }
  
  .product-card {
    max-width: 180px;
  }
  
  .product-image {
    height: 160px;
  }
}
</style>