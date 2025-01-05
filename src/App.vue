<template>
  <el-config-provider size="small" :locale="zhCn">
    <!-- 导航栏 -->
    <nav-bar
      v-if="route.meta.isShowComNav"
      :key="refreshUuid"
      bg-color="#fff"
      font-color="green"
      position="sticky"
      icon-color="green"
    ></nav-bar>
    <router-view v-show="!isLoading" v-slot="{}" :key="refreshUuid"></router-view>
    <loading-com-vue v-show="isLoading"></loading-com-vue>
  </el-config-provider>
</template>
<script lang="ts" setup>
  import LoadingComVue from '@/components/Loading/LoadingCom.vue'; // 全局等待层

  import appStore from './store';
  import { storeToRefs } from 'pinia';
  // import { openAndCloseLoadingByTime } from './utils/common';
  import zhCn from 'element-plus/es/locale/lang/zh-cn';
  import { addWebsiteViewsAsync } from './http/api/panel';
  import { useHead } from '@vueuse/head';
  useHead({
    meta: [
      {
        name: 'description',
        content: '职行AI简历- AI简历制作神器！'
      },
      {
        name: 'keywords',
        content: '简历 AI'
      }
    ]
  });

  const { isLoading } = storeToRefs(appStore.useLoadingStore);
  // openAndCloseLoadingByTime(1500); // 等待动画层
  const { refreshUuid } = appStore.useRefreshStore;
  const route = useRoute();

  // 查询网站配置
  const { getWebsiteConfig } = appStore.useWebsiteConfigStore;
  getWebsiteConfig();
</script>
<style>
  /* 设置了打印会出现问题 */
  #app {
    /* min-width: 1300px; */
  }
</style>
