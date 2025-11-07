<template>
  <div class="sound-product-container">
    <el-card title="声音产品管理">
      <div class="sound-editor">
        <!-- 录音功能区 -->
        <div class="record-section">
          <el-button type="primary" @click="startRecord" :disabled="isRecording">
            <el-icon><Microphone /></el-icon> 开始录音
          </el-button>
          <el-button type="danger" @click="stopRecord" :disabled="!isRecording">
            <el-icon><MicrophoneOff /></el-icon> 停止录音
          </el-button>
          <el-button type="success" @click="playRecord" :disabled="!recordedBlob">
            <el-icon><VideoPlay /></el-icon> 播放录音
          </el-button>
          <el-button type="warning" @click="clearRecord" :disabled="!recordedBlob">
            <el-icon><Delete /></el-icon> 清除录音
          </el-button>
        </div>

        <!-- 商品音频说明 -->
        <div class="product-info-section">
          <el-form-item label="对应商品">
            <el-input v-model="productInfo" placeholder="请输入商品名称或ID" />
          </el-form-item>
        </div>

        <!-- 音频编辑区 -->
        <div class="edit-section" v-if="recordedBlob">
          <el-card title="音频编辑">
            <div class="edit-tools">
              <el-button type="primary" @click="showEditDialog = true">
                <el-icon><Edit /></el-icon> 编辑声音
              </el-button>
              <el-button type="success" @click="saveSound">
                <el-icon><Download /></el-icon> 保存为MP4
              </el-button>
            </div>
          </el-card>
        </div>

        <!-- 编辑对话框 -->
        <el-dialog
          title="音频编辑"
          v-model="showEditDialog"
          width="800px"
          @close="resetEdit"
        >
          <div class="edit-dialog-content">
            <!-- 裁剪功能 -->
            <el-card title="裁剪音频">
              <div class="crop-section">
                <el-slider
                  v-model="cropRange"
                  :min="0"
                  :max="audioDuration"
                  range
                  @change="onCropChange"
                />
                <div class="crop-time">
                  <span>开始时间: {{ formatTime(cropRange[0]) }}</span>
                  <span>结束时间: {{ formatTime(cropRange[1]) }}</span>
                </div>
              </div>
            </el-card>

            <!-- 插入声音功能 -->
            <el-card title="插入声音">
              <div class="insert-section">
                <el-form-item label="插入位置">
                  <el-slider
                    v-model="insertPosition"
                    :min="0"
                    :max="audioDuration"
                  />
                  <span>{{ formatTime(insertPosition) }}</span>
                </el-form-item>
                <el-form-item label="文字转语音">
                  <el-input
                    v-model="textToSpeech"
                    placeholder="请输入要转换的文字"
                    type="textarea"
                    rows="3"
                  />
                </el-form-item>
                <el-button type="primary" @click="convertTextToSpeech" :disabled="!textToSpeech">
                  <el-icon><Music /></el-icon> 转换为语音
                </el-button>
                <div v-if="convertedAudio" class="converted-audio">
                  <audio :src="convertedAudio" controls />
                  <el-button type="success" @click="insertAudio">插入到音频</el-button>
                  <el-button type="danger" @click="deleteConvertedAudio">删除</el-button>
                </div>
              </div>
            </el-card>

            <!-- 编辑文字 -->
            <el-card title="编辑文字">
              <div class="text-edit-section">
                <el-input
                  v-model="audioText"
                  placeholder="请输入音频说明文字"
                  type="textarea"
                  rows="5"
                />
              </div>
            </el-card>
          </div>
          <template #footer>
            <div class="dialog-footer">
              <el-button @click="showEditDialog = false">取消</el-button>
              <el-button type="primary" @click="applyEdit">应用编辑</el-button>
            </div>
          </template>
        </el-dialog>
      </div>
    </el-card>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import { Microphone, VideoPlay, Delete, Edit, Download } from '@element-plus/icons-vue'

// 录音状态
const isRecording = ref(false)
const recordedBlob = ref(null)
const productInfo = ref('')
const showEditDialog = ref(false)

// 音频编辑
const audioDuration = ref(100) // 模拟音频时长
const cropRange = ref([0, 100])
const insertPosition = ref(50)
const textToSpeech = ref('')
const convertedAudio = ref(null)
const audioText = ref('')

// 开始录音
const startRecord = () => {
  isRecording.value = true
  // 这里需要实现真正的录音功能
  console.log('开始录音')
}

// 停止录音
const stopRecord = () => {
  isRecording.value = false
  // 这里需要实现真正的录音功能
  recordedBlob.value = new Blob() // 模拟录音结果
  console.log('停止录音')
}

// 播放录音
const playRecord = () => {
  // 这里需要实现真正的播放功能
  console.log('播放录音')
}

// 清除录音
const clearRecord = () => {
  recordedBlob.value = null
  console.log('清除录音')
}

// 保存声音
const saveSound = () => {
  // 这里需要实现真正的保存功能
  console.log('保存为MP4')
}

// 转换文字为语音
const convertTextToSpeech = () => {
  // 这里需要实现真正的文字转语音功能
  convertedAudio.value = 'audio-url' // 模拟转换结果
  console.log('文字转语音')
}

// 插入音频
const insertAudio = () => {
  // 这里需要实现真正的插入功能
  console.log('插入音频')
}

// 删除转换的音频
const deleteConvertedAudio = () => {
  convertedAudio.value = null
  console.log('删除转换的音频')
}

// 应用编辑
const applyEdit = () => {
  // 这里需要实现真正的编辑应用功能
  showEditDialog.value = false
  console.log('应用编辑')
}

// 重置编辑
const resetEdit = () => {
  cropRange.value = [0, audioDuration.value]
  insertPosition.value = 50
  textToSpeech.value = ''
  convertedAudio.value = null
  audioText.value = ''
}

// 格式化时间
const formatTime = (seconds) => {
  const mins = Math.floor(seconds / 60)
  const secs = Math.floor(seconds % 60)
  return `${mins}:${secs.toString().padStart(2, '0')}`
}

// 裁剪变化
const onCropChange = () => {
  console.log('裁剪范围变化', cropRange.value)
}
</script>

<style scoped>
.sound-product-container {
  padding: 20px;
}

.sound-editor {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.record-section {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}

.product-info-section {
  margin-top: 20px;
}

.edit-section {
  margin-top: 20px;
}

.edit-tools {
  display: flex;
  gap: 10px;
}

.edit-dialog-content {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.crop-section {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.crop-time {
  display: flex;
  justify-content: space-between;
  font-size: 14px;
  color: #666;
}

.insert-section {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.converted-audio {
  display: flex;
  gap: 10px;
  align-items: center;
  margin-top: 10px;
}

.text-edit-section {
  margin-top: 10px;
}
</style>