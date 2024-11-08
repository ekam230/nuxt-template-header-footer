<template>
  <div class="min-h-screen bg-gray-50 flex flex-col">
    <AppMenu />
    <main class="container mx-auto p-4 flex-grow">
      <slot />
    </main>
    <AppFooter />
  </div>
</template>