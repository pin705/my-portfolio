<script lang="ts" setup>
import type { Stats } from '~~/types'

const { data: stats } = await useFetch<Stats>('/api/stats')
const { t } = useI18n({
  useScope: 'local'
})
</script>

<template>
  <ClientOnly>
    <i18n-t
      v-if="stats"
      keypath="stats"
      tag="p"
    >
      <template #time>
        {{ useTimeAgo(new Date(stats.coding.data.range.start)).value }}
      </template>
      <template #date>
        <HoverText
          :hover="t('tooltip.date')"
          :text="useDateFormat(new Date(stats.coding.data.range.start), 'Do MMMM YYYY').value"
        />
      </template>
      <template #hours>
        <HoverText
          :hover="t('tooltip.hours')"
          :text="usePrecision(stats.coding.data.grand_total.total_seconds_including_other_language / 3600, 0).value"
        />
      </template>
      <template #editors>
        {{ stats.editors.data.slice(0, 2).map(editor => `${editor.name} (${editor.percent}%)`).join(' and ') }}
      </template>
      <template
        v-if="stats.os.data[0]"
        #os
      >
        {{ stats.os.data[0].name }} ({{ stats.os.data[0].percent }}%)
      </template>
      <template #languages>
        {{
          stats.languages.data.slice(0, 2).map(language => `${language.name} (${language.percent}%)`).join(t('separator'))
        }}
        {{ stats.languages.data.slice(0, 2).map(language => `${language.name} (${language.percent}%)`).join(t('separator')) }}
      </template>
    </i18n-t>
  </ClientOnly>
</template>

<i18n lang="json">
{
  "en": {
    "stats": "I collect some data for {time}, started the {date}. I've coded for a total of {hours} hours. My best editors are {editors}. My best OS is {os}. My top languages are {languages}.",
    "separator": " and ",
    "tooltip": {
      "date": "That was so long ago 🫣",
      "hours": "That's a lot 😮"
    }
  },
"vi": {
  "stats": "Tôi đã thu thập một số dữ liệu trong {time}, bắt đầu từ {date}. Tôi đã lập trình tổng cộng {hours} giờ. Trình soạn thảo tốt nhất của tôi là {editors}. Hệ điều hành tốt nhất của tôi là {os}. Ngôn ngữ lập trình hàng đầu của tôi là {languages}.",
  "separator": " và ",
  "tooltip": {
    "date": "Đã lâu rồi 🫣",
    "hours": "Đó là rất nhiều 😮"
  }
}
}
</i18n>
