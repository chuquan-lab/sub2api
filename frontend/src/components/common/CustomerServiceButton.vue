<template>
  <button
    type="button"
    :class="buttonClass"
    :title="t('common.customerService.open')"
    :aria-label="t('common.customerService.open')"
    @click="showDialog = true"
  >
    <Icon name="user" :size="iconSize" />
    <span v-if="showLabel" class="hidden sm:inline">{{ t('common.customerService.label') }}</span>
  </button>

  <BaseDialog
    :show="showDialog"
    :title="t('common.customerService.title')"
    width="narrow"
    close-on-click-outside
    @close="showDialog = false"
  >
    <div class="space-y-4 text-center">
      <img
        :src="customerServiceQrUrl"
        :alt="t('common.customerService.imageAlt')"
        class="mx-auto aspect-square w-full max-w-[320px] rounded-lg border border-gray-200 bg-white object-cover dark:border-dark-700"
      />
      <p class="text-sm font-medium text-gray-700 dark:text-dark-200">
        {{ t('common.customerService.scanHint') }}
      </p>
    </div>
  </BaseDialog>
</template>

<script setup lang="ts">
import { computed, ref } from 'vue'
import { useI18n } from 'vue-i18n'
import BaseDialog from '@/components/common/BaseDialog.vue'
import Icon from '@/components/icons/Icon.vue'

const props = withDefaults(defineProps<{
  variant?: 'icon' | 'nav'
}>(), {
  variant: 'icon'
})

const { t } = useI18n()

const showDialog = ref(false)
const customerServiceQrUrl = 'https://chuquan-public-r-001.oss-cn-shanghai.aliyuncs.com/onetokenicu/one-token-icu.png'

const showLabel = computed(() => props.variant === 'nav')
const iconSize = computed(() => props.variant === 'nav' ? 'sm' : 'md')

const buttonClass = computed(() => props.variant === 'nav'
  ? 'flex items-center gap-1.5 rounded-lg px-2.5 py-1.5 text-sm font-medium text-gray-600 transition-colors hover:bg-gray-100 hover:text-gray-900 dark:text-dark-400 dark:hover:bg-dark-800 dark:hover:text-white'
  : 'rounded-lg p-2 text-gray-500 transition-colors hover:bg-gray-100 hover:text-gray-700 dark:text-dark-400 dark:hover:bg-dark-800 dark:hover:text-white'
)
</script>
