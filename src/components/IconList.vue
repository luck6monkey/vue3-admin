<template>
  <div class="icon-list">
    <h2>Element Plus Icons List</h2>
    <div class="icons-container">
      <div v-for="iconName in iconNames" :key="iconName" class="icon-item">
        <el-icon :size="32"><component :is="ElIcons[iconName]" /></el-icon>
        <span>{{ iconName }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import * as ElIcons from '@element-plus/icons-vue'

const iconNames = Object.keys(ElIcons)
</script>

<style scoped>
.icon-list {
  padding: 20px;
}

.icons-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.icon-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5px;
  padding: 10px;
  border: 1px solid #eee;
  border-radius: 5px;
  width: 120px;
  text-align: center;
}

.icon-item span {
  font-size: 12px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  width: 100%;
}
</style>