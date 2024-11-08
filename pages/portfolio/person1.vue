<template>
  <div class="max-w-4xl mx-auto">
    <h1 class="text-4xl font-bold mb-6">Person 1's Portfolio</h1>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
      <div class="bg-white rounded-lg shadow-md overflow-hidden">
        <LazyImage
          src="https://images.unsplash.com/photo-1544005313-94ddf0286df2?auto=format&fit=crop&w=800&q=80"
          alt="Project 1"
          :aspect-ratio="75"
        />
        <div class="p-6">
          <h3 class="text-xl font-semibold mb-2">Project 1</h3>
          <p class="text-gray-600">A showcase of innovative design and functionality.</p>
        </div>
      </div>
      <div class="bg-white rounded-lg shadow-md overflow-hidden">
        <LazyImage
          src="https://images.unsplash.com/photo-1554774853-aae0a22c8aa4?auto=format&fit=crop&w=800&q=80"
          alt="Project 2"
          :aspect-ratio="75"
        />
        <div class="p-6">
          <h3 class="text-xl font-semibold mb-2">Project 2</h3>
          <p class="text-gray-600">Creative solutions for modern challenges.</p>
        </div>
      </div>
    </div>
  </div>
</template>