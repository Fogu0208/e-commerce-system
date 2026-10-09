<template>
  <div class="quicknav">
    <!-- 返回顶部：滚动超过 300px 触发，保留淡入淡出动画 -->
    <transition name="quicknav-fade">
      <a
          v-show="showTop"
          href="javascript:void(0)"
          class="quicknav-item"
          @click="scrollToTop"
          title="返回顶部"
      >
        <el-icon :size="20"><Top /></el-icon>
      </a>
    </transition>
    <router-link to="/cart" class="quicknav-item" title="购物车">
      <el-icon :size="20"><ShoppingCart /></el-icon>
      <span class="tip">购物车</span>
    </router-link>
    <router-link to="/userinfo" class="quicknav-item" title="个人信息">
      <el-icon :size="20"><User /></el-icon>
      <span class="tip">个人信息</span>
    </router-link>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { ShoppingCart, User, Top } from '@element-plus/icons-vue'

const showTop = ref(false)

const scrollToTop = () => window.scrollTo({ top: 0, behavior: 'smooth' })

const handler = () => {
  showTop.value = window.scrollY > 300
}
onMounted(() => {
  window.addEventListener('scroll', handler, { passive: true })
})
onUnmounted(() => window.removeEventListener('scroll', handler))
</script>

<style>
.quicknav { position: fixed; right: 16px; bottom: 120px; z-index: 99; display: flex; flex-direction: column; gap: 2px; }
.quicknav-item { width: 44px; height: 44px; display: flex; align-items: center; justify-content: center;
  background: #fff; border: 1px solid #e8e8e8; border-radius: 8px; color: #666; text-decoration: none;
  position: relative; transition: all .2s; }
.quicknav-item:hover { color: #A10000; border-color: #A10000; background: #fef5f5; box-shadow: 0 2px 8px rgba(161,0,0,0.1); }
.quicknav-item .tip { position: absolute; right: 54px; background: #333; color: #fff; font-size: 12px;
  padding: 4px 10px; border-radius: 4px; white-space: nowrap; opacity: 0; pointer-events: none; transition: opacity .2s; }
.quicknav-item:hover .tip { opacity: 1; }

/* 仅针对“返回顶部”的淡入淡出动画 */
.quicknav-fade-enter-active, .quicknav-fade-leave-active { transition: opacity .3s, transform .3s; }
.quicknav-fade-enter-from, .quicknav-fade-leave-to { opacity: 0; transform: translateY(10px); }
</style>
