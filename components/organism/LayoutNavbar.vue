<script setup lang="ts">
import { ROUTE_PATHS } from '~/constants/routes';

const props = defineProps<{
  type: 'header' | 'mobile-header' | 'footer';
  navClass: string;
}>();

const dialogStore = useDialogStore();

const { tm } = useI18n();

// 計算不同類型的 nav-item class
const navItemClass = computed(() => {
  const typeMap: Record<string, string> = {
    header: 'header-nav-item',
    'mobile-header': 'mobile-header-nav-item',
    footer: 'footer-nav-item',
  };
  return typeMap[props.type] || '';
});

// 計算 v-kb-focus 的 Y 座標，避免重複計算
const kbFocusY = computed(() => (props.type === 'header' ? 1 : 202));

// 定義導覽項目介面
interface NavItem {
  text: string;
  path: string; // 用於 NuxtLink 的 'to' 或 <a> 的 'href'
  isExternal: boolean;
  target?: string; // 外部連結可能需要 target 屬性
}

// 導覽項目列表，使用 computed 以確保 i18n 內容更新時也能反應
const navItems = computed<NavItem[]>(() => [
  {
    text: '競賽規則',
    path: ROUTE_PATHS.RULES,
    isExternal: false,
  },
  {
    text: '重要時程',
    path: `${ROUTE_PATHS.RULES}${ROUTE_PATHS.SCHEDULE}`,
    isExternal: false,
  },
  {
    text: 'FAQ',
    path: `${ROUTE_PATHS.RULES}${ROUTE_PATHS.FAQ}`,
    isExternal: false,
  },
  {
    text: '參賽回顧',
    path: ROUTE_PATHS.PAST,
    isExternal: false,
  },
  {
    text: '歷屆紀錄',
    path: tm('past_url'), // 假設 tm('past_url') 返回的是 URL 字串
    isExternal: true,
    target: '_blank',
  },
]);
</script>

<template>
  <nav>
    <ul :class="navClass">
      <li v-for="(item, index) in navItems" :key="item.text" :class="navItemClass">
        <component
          :is="item.isExternal ? 'a' : 'NuxtLink'"
          v-kb-focus="{
            id: `${type}-nav${index + 2}-${kbFocusY}`, // x 座標從 2 開始，id 也要對應
            x: index + 2, // 根據迴圈索引動態計算 x 座標
            y: kbFocusY,
          }"
          :[item.isExternal ? 'href' : 'to']="item.path"
          :target="item.target"
          @click="dialogStore.closeDialog()"
        >
          {{ item.text }}
        </component>
      </li>
    </ul>
  </nav>
</template>

<style scoped lang="postcss">
.header-nav-item {
  @apply px-4;
}

.footer-nav-item {
  @apply pr-4 py-2;
}

.mobile-header-nav-item {
  @apply p-8 border-b border-b-white last:border-b-0;
}
</style>