<template>
  <header class="header">
    <section class="main">
      <h1>
        <img src="./assets/images/logo.webp" />
        PayQrcode
      </h1>
      <h2>二合一收款码物理合并版</h2>
    </section>
  </header>
  <main>
    <<t-space direction="vertical">
      <<t-alert theme="info">
        <template #message>
          支持一下：
          <<t-link
            theme="primary"
            underline
            @click.stop="showRewardModal = true"
            style="cursor: pointer;"
          >
            打赏
          </</t-link>
          ，资源网：
          <<t-link theme="primary" underline href="https://m.chaoyuevip.cn" target="_blank">
            博客
          </</t-link>
        </template>
      </</t-alert>
      <<t-alert theme="success">
        <template #icon></template>
        <template #message>
          <p>
            ✅ 物理合并，直接将图片合并成一张图片，无需服务器，不怕被篡改，可打印使用，稳定，绿色，安全！
          </p>
          <p>⚠️全程离线运行，二维码解析合并无任何更改，且项目开源，请放心食用！</p>
        </template>
      </</t-alert>
      <<t-alert theme="warning" message="请尽量把非二维码区域裁剪后上传，以提升识别准确性！" />
    </</t-space>
    <Main />
  </main>

  <!-- 打赏收款码弹窗 -->
  <teleport to="body">
    <!-- 1. 弹窗遮罩层 -->
    <div class="reward-modal-mask" v-if="showRewardModal" @click="showRewardModal = false">
      <div class="reward-modal-content" @click.stop>
        <h3 class="reward-modal-title">感谢您的支持！</h3>
        <p class="reward-modal-desc">扫码即可完成打赏（支持微信/支付宝）<br>点击图片可放大查看</p>
        <!-- 2. 可点击放大的收款码图片 -->
        <div 
          class="reward-qrcode-container"
          @click="isQrcodeZoomed = !isQrcodeZoomed"
        >
          <img 
            src="https://qq626810248.oss-cn-beijing.aliyuncs.com-cE5%9B%BE%E7%89%87/ds.png" 
            alt="打赏收款码" 
            class="reward-qrcode"
            :class="{ 'reward-qrcode--zoomed': isQrcodeZoomed }"
            :style="{ cursor: isQrcodeZoomed ? 'zoom-out' : 'zoom-in' }"
          >
        </div>
        <button class="reward-close-btn" @click="showRewardModal = false">关闭</button>
      </div>
    </div>
  </teleport>
</template>

<script lang="ts" setup>
import Main from '@/components/Main/Main.vue'
import { ref } from 'vue'

// 控制弹窗显示/隐藏
const showRewardModal = ref(false)
// 控制收款码是否放大
const isQrcodeZoomed = ref(false)

// 监听弹窗关闭，同时重置图片放大状态
watch(showRewardModal, (newVal) => {
  if (!newVal) isQrcodeZoomed.value = false
})
</script>

<style scoped>
/* 弹窗遮罩层 */
.reward-modal-mask {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.6);
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* 弹窗内容区 */
.reward-modal-content {
  background: #fff;
  padding: 24px;
  border-radius: 8px;
  width: 90%;
  max-width: 350px;
  text-align: center;
  box-sizing: border-box;
}

/* 弹窗标题 */
.reward-modal-title {
  margin: 0 0 12px;
  font-size: 18px;
  color: #333;
}

/* 弹窗描述 */
.reward-modal-desc {
  margin: 0 0 16px;
  font-size: 14px;
  color: #666;
  line-height: 1.5;
}

/* 收款码容器（控制放大时不溢出） */
.reward-qrcode-container {
  width: 100%;
  max-width: 280px;
  margin: 0 auto 20px;
  overflow: hidden;
  border-radius: 4px;
}

/* 收款码基础样式 */
.reward-qrcode {
  width: 100%;
  height: auto;
  border: 1px solid #eee;
  transition: transform 0.3s ease; /* 平滑放大过渡 */
}

/* 收款码放大样式 */
.reward-qrcode--zoomed {
  transform: scale(1.8); /* 放大1.8倍，可根据需求调整 */
  transform-origin: center; /* 从中心放大 */
}

/* 关闭按钮 */
.reward-close-btn {
  padding: 8px 28px;
  border: none;
  border-radius: 4px;
  background: #07C160;
  color: #fff;
  font-size: 14px;
  cursor: pointer;
  transition: background 0.2s;
}

.reward-close-btn:hover {
  background: #06b355;
}
</style>
