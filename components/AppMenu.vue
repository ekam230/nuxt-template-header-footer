<template>
  <nav class="bg-white shadow-md p-4">
    <div class="container mx-auto">
      <div class="flex flex-wrap items-center justify-between">
        <NuxtLink to="/" class="text-xl font-bold text-gray-800">My Site</NuxtLink>
        <button 
          @click="isOpen = !isOpen" 
          class="lg:hidden p-2 rounded-md hover:bg-gray-100"
        >
          <span class="block w-6 h-0.5 bg-gray-600 mb-1"></span>
          <span class="block w-6 h-0.5 bg-gray-600 mb-1"></span>
          <span class="block w-6 h-0.5 bg-gray-600"></span>
        </button>
        <div 
          :class="[
            'lg:flex lg:space-x-4',
            isOpen ? 'block' : 'hidden',
            'w-full lg:w-auto mt-4 lg:mt-0'
          ]"
        >
          <template v-for="item in menuItems" :key="item.path">
            <!-- Regular menu items -->
            <template v-if="!item.children">
              <NuxtLink 
                :to="item.path"
                class="nav-link block lg:inline-block py-2 lg:py-0"
              >
                {{ item.name }}
              </NuxtLink>
            </template>
            
            <!-- Dropdown menu items -->
            <div v-else class="relative group" @mouseenter="item.isOpen = true" @mouseleave="item.isOpen = false">
              <button 
                class="nav-link block lg:inline-block py-2 lg:py-0 w-full lg:w-auto text-left"
                @click="item.isOpen = !item.isOpen"
              >
                {{ item.name }}
                <span class="ml-1">▼</span>
              </button>
              
              <div 
                v-show="item.isOpen"
                class="lg:absolute left-0 mt-2 lg:mt-0 w-48 bg-white rounded-md shadow-lg py-1 z-50"
              >
                <NuxtLink
                  v-for="child in item.children"
                  :key="child.path"
                  :to="child.path"
                  class="block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100"
                  @click="item.isOpen = false"
                >
                  {{ child.name }}
                </NuxtLink>
              </div>
            </div>
          </template>
        </div>
      </div>
    </div>
  </nav>
</template>

<script setup>
const isOpen = ref(false);

const menuItems = reactive([
  { name: 'Home', path: '/' },
  { name: 'About', path: '/about' },
  { name: 'Services', path: '/services' },
  { 
    name: 'Portfolio',
    path: '/portfolio',
    isOpen: false,
    children: [
      { name: 'Person 1', path: '/portfolio/person1' },
      { name: 'Person 2', path: '/portfolio/person2' }
    ]
  },
  { name: 'Team', path: '/team' },
  { name: 'Blog', path: '/blog' },
  { name: 'Contact', path: '/contact' },
  { name: 'Pricing', path: '/pricing' },
  { name: 'FAQ', path: '/faq' },
  { name: 'Careers', path: '/careers' }
]);
</script>

<style scoped>
.nav-link {
  @apply text-gray-600 hover:text-gray-900 px-2 py-1 rounded-md hover:bg-gray-100 transition-colors;
}
</style>