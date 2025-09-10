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
    <!-- 公告弹窗 -->
    <<t-dialog
      v-model="isNoticeShow"
      title="📢 最新公告"
      width="500px"
      :close-on-click-outside="false"
    >
      <div class="notice-content">
        <p>1. 【功能更新】新增二维码清晰度优化功能，合并后支持高清导出</p>
        <p>2. 【温馨提示】建议使用 Chrome 或 Edge 浏览器，避免兼容性问题</p>
        <p>3. 【资源更新】博客新增「二维码设计教程」，欢迎前往学习</p>
      </div>
      <template #footer>
        <<t-button theme="primary" @click="isNoticeShow = false">我知道了</</t-button>
      </template>
    </</t-dialog>

    <<t-space direction="vertical">
      <<t-alert theme="info">
        <template #message>
          支持一下：
          <<t-link
            theme="primary"
            underline
            href="https://qq626810248.oss-cn-beijing.aliyuncs.com-cE5%9B%BE%E7%89%87/ds.png"
            target="_blank"
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
<p>⚠️上传官方支付宝和微信收款码，选择喜欢的收款码主题背景，生成好的收款码一定要用支付宝和微信扫码测试一下，如测试识别收款码有识，尝试调节缺省比例重新生成，自己支付宝扫码收款码会跳转到支付宝今日收款界面那是正确的收款码</p>
        </template>
      </</t-alert>
      <<t-alert theme="warning" message="请尽量把非二维码区域裁剪后上传，以提升识别准确性！" />
    </</t-space>
    <Main />
  </main>
</template>

<script lang="ts" setup>
import Main from '@/components/Main/Main.vue'
import { ref } from 'vue'
// 控制公告弹窗显示/隐藏的状态
const isNoticeShow = ref(true)
</script>

<style scoped>
/* 公告内容样式优化，增加行间距 */
.notice-content {
  line-height: 1.8;
  color: #333;
}
.notice-content p {
  margin: 8px 0;
}
</style>
