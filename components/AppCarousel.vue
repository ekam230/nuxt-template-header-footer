<template>
  <div class="relative w-full h-[400px] overflow-hidden">
    <ClientOnly>
      <div class="flex transition-transform duration-500 h-full" :style="{ transform: `translateX(-${currentSlide * 100}%)` }">
        <div v-for="(slide, index) in slides" :key="index" class="min-w-full h-full">
          <div class="w-full h-full relative">
            <LazyImage
              :src="slide.image"
              :alt="slide.title"
              :aspect-ratio="56.25"
              class="absolute inset-0"
            />
            <div class="absolute inset-0 bg-black/40 flex items-center justify-center">
              <div class="text-center text-white">
                <h2 class="text-3xl font-bold mb-4">{{ slide.title }}</h2>
                <p class="text-xl">{{ slide.description }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <button @click="prevSlide" class="absolute left-4 top-1/2 transform -translate-y-1/2 bg-white/80 p-2 rounded-full hover:bg-white/90 transition-colors">
        <span class="block w-6 h-6">←</span>
      </button>
      
      <button @click="nextSlide" class="absolute right-4 top-1/2 transform -translate-y-1/2 bg-white/80 p-2 rounded-full hover:bg-white/90 transition-colors">
        <span class="block w-6 h-6">→</span>
      </button>
      
      <div class="absolute bottom-4 left-1/2 transform -translate-x-1/2 flex space-x-2">
        <button 
          v-for="(_, index) in slides" 
          :key="index"
          @click="currentSlide = index"
          class="w-3 h-3 rounded-full transition-colors"
          :class="currentSlide === index ? 'bg-white' : 'bg-white/50'"
        ></button>
      </div>
    </ClientOnly>
  </div>
</template>

<script setup>
const slides = ref([
  {
    title: "Welcome to Our Platform",
    description: "Discover amazing features and services",
    image: "https://images.unsplash.com/photo-1451187580459-43490279c0fa?auto=format&fit=crop&w=1200&q=80"
  },
  {
    title: "Professional Solutions",
    description: "Tailored to your needs",
    image: "https://images.unsplash.com/photo-1504384764586-bb4cdc1707b0?auto=format&fit=crop&w=1200&q=80"
  },
  {
    title: "24/7 Support",
    description: "We're here to help you succeed",
    image: "https://images.unsplash.com/photo-1557426272-fc759fdf7a8d?auto=format&fit=crop&w=1200&q=80"
  }
]);

const currentSlide = ref(0);

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % slides.value.length;
};

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + slides.value.length) % slides.value.length;
};

// Auto-advance slides only on client side
onMounted(() => {
  const interval = setInterval(nextSlide, 5000);
  onUnmounted(() => clearInterval(interval));
});
</script>