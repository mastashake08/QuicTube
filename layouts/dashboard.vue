<template>
  <UDashboardLayout>
    <UDashboardPanel :width="250" :resizable="{ min: 200, max: 300 }" collapsible>
      <UDashboardNavbar />

      <UDashboardSidebar>
        <template #header>
          <UDashboardSearchButton />
        </template>

        <UDashboardSidebarLinks />
      </UDashboardSidebar>
    </UDashboardPanel>

    <slot />

    <UDashboardSearch />
  </UDashboardLayout>
</template>
