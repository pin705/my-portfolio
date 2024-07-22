<template>
  <div class="flex items-center gap-2 mt-4">
    <div class="flex items-center">
      <UTooltip text="It's me 👋">
        <div class="flex items-center w-12 h-12">
          <NuxtImg
            alt="Pin picture"
            class="w-full h-full hover:rotate-[360deg] duration-500 transform-gpu"
            src="/favicon.png"
          />
        </div>
      </UTooltip>
    </div>
    <p class="not-prose">
      {{ t('quote') }}
    </p>
  </div>
</template>

<script lang="ts" setup>
const { t } = useI18n({
  useScope: 'local'
})
</script>

<i18n lang="json">
{
  "en": {
    "quote": "Hello everyone! Thanks for visiting my portfolio. Please leave whatever you like to say, such as suggestions, appreciations, questions or anything!"
  },
  "vi": {
  "quote": "Xin chào mọi người! Cảm ơn bạn đã ghé thăm danh mục của tôi. Hãy để lại bất cứ điều gì bạn muốn nói, chẳng hạn như gợi ý, lời cảm ơn, câu hỏi hoặc bất cứ điều gì khác!"
}
}
</i18n>
