<script setup lang="ts">
import type { BlogPost } from '~/types'
const layout = 'dashboard'
const { data: page } = await useAsyncData('videos', () => queryContent('/videos').findOne())
if (!page.value) {
  throw createError({ statusCode: 404, statusMessage: 'Page not found', fatal: true })
}

const { data: posts } = await useAsyncData('posts', () => queryContent<BlogPost>('/videos')
  .where({ _extension: 'md' })
  .sort({ date: -1 })
  .find())

useSeoMeta({
  title: page.value.title,
  ogTitle: page.value.title,
  description: page.value.description,
  ogDescription: page.value.description
})

defineOgImage({
  component: 'Saas',
  title: page.value.title,
  description: page.value.description
})
</script>

<template>
  <NuxtLayout :layout="layout">
    <UContainer>
      <UPage>
        <template #left>
          <UAside>
            <template #top>
              <UContentSearchButton
                class="rounded-md"
                size="sm"
              />
            </template>

            <UNavigationTree :links="mapContentNavigation(links)" />
          </UAside>
        </template>

        <NuxtPage />
      </UPage>
    </UContainer>
  </NuxtLayout>
</template>
