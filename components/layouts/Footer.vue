<script setup lang="ts">
const runtimeConfig = useRuntimeConfig();
const {ja, en} = runtimeConfig.public.footer;

const html: any = {
  ja,
  en,
};
</script>

<template>
  <div class="bg-primary text-center py-5" v-html="html[$i18n.locale]"></div>
</template>
