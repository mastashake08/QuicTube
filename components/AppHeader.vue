<script setup lang="ts">
import type { NavItem } from '@nuxt/content/dist/runtime/types'

const navigation = inject<Ref<NavItem[]>>('navigation', ref([]))

const links = [{
  label: 'Try Now',
  to: '/try-now'
},{
  label: 'Docs',
  to: '/docs'
}, {
  label: 'Pricing',
  to: '/pricing'
}, {
  label: 'Blog',
  to: '/blog'
}]
</script>

<template>
  <UHeader :links="links">
    <template #logo>
      QuicTube <UBadge
        label="Powered By QUIC"
        variant="subtle"
        class="mb-0.5"
      />
    </template>

    <template #right>
      <UButton
        label="Sign in"
        color="gray"
        to="/login"
      />
      <UButton
        label="Sign up"
        icon="i-heroicons-arrow-right-20-solid"
        trailing
        color="black"
        to="/signup"
        class="hidden lg:flex"
      />
    </template>

    <template #panel>
      <h2>The tech stack I used!</h2>
      <UNavigationTree
        :links="mapContentNavigation(navigation)"
        default-open
      />
    </template>
  </UHeader>
</template>
