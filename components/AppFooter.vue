<script setup lang="ts">
const links = [{
  label: 'Resources',
  children: [{
    label: 'Help center'
  }, {
    label: 'Docs',
    to: '/docs'
  }, {
    label: 'Roadmap'
  }, {
    label: 'Changelog'
  }]
}, {
  label: 'Features',
  children: [{
    label: 'Affiliates'
  }, {
    label: 'Portal'
  }]
}, {
  label: 'Product',
  children: [{
    label: 'About'
  }, {
    label: 'Pricing',
    to: '/pricing'
  }, {
    label: 'Blog',
    to: '/blog'
  }]
}]

const toast = useToast()

const email = ref('')
const loading = ref(false)

function onSubmit() {
  loading.value = true

  setTimeout(() => {
    toast.add({
      title: 'Subscribed!',
      description: 'You\'ve been subscribed to our newsletter.'
    })

    loading.value = false
  }, 1000)
}
</script>

<template>
  <UFooter>
    <template #top>
      <UFooterColumns :links="links">
        <ULandingSection
          title="The tech stack I used!"
          description="All open source of course" />
        <template #right>
          
        </template>
      </UFooterColumns>
    </template>

    <template #left>
      <p class="text-gray-500 dark:text-gray-400 text-sm">
        Copyright QuicTube © {{ new Date().getFullYear() }}. All rights reserved.
      </p>
    </template>

    <template #right>
      <UColorModeButton size="sm" />

      <UButton
        to="https://github.com/mastashake08/QuicTube"
        target="_blank"
        icon="i-simple-icons-github"
        aria-label="GitHub"
        color="gray"
        variant="ghost"
      />

      <UButton
        to="https://twitter.com/jyroneparker"
        target="_blank"
        icon="i-simple-icons-x"
        aria-label="X"
        color="gray"
        variant="ghost"
      />

      <UButton
        to="https://open.spotify.com/artist/1nQuAaO8h98RiBdzfMhlSu?si=7XFtqiF_ShurTO-2r0Xy_Q"
        target="_blank"
        icon="i-simple-icons-spotify"
        aria-label="X"
        color="gray"
        variant="ghost"
      />
      
      <UButton
        to="https://instagram.com/mastashake08"
        target="_blank"
        icon="i-simple-icons-instagram"
        aria-label="Instagram"
        color="gray"
        variant="ghost"
      />

      <UButton
        to="https://jyroneparker.com"
        target="_blank"
        icon="i-simple-icons-wordpress"
        aria-label="Personal Website"
        color="gray"
        variant="ghost"
      />

      <UButton
        to="https://cashapp.me/$mastashake08"
        target="_blank"
        icon="i-simple-icons-cashapp"
        aria-label="Cash App"
        color="gray"
        variant="ghost"
      />
    </template>
  </UFooter>
</template>
