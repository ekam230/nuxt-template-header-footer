<template>
  <ClientOnly>
    <div class="relative overflow-hidden" :style="{ paddingBottom: `${aspectRatio}%` }">
      <!-- Loading placeholder -->
      <div
        v-if="loading"
        class="absolute inset-0 bg-gray-200 animate-pulse"
      ></div>
      
      <!-- Actual image -->
      <img
        ref="imageRef"
        :data-src="src"
        :alt="alt"
        class="absolute inset-0 w-full h-full object-cover transition-opacity duration-300"
        :class="{ 'opacity-0': loading, 'opacity-100': !loading }"
        @load="onImageLoad"
        @error="onImageError"
      />
      
      <!-- Error state -->
      <div
        v-if="error"
        class="absolute inset-0 flex items-center justify-center bg-gray-100"
      >
        <span class="text-gray-400">Failed to load image</span>
      </div>
    </div>
  </ClientOnly>
</template>

<script setup>
const props = defineProps({
  src: {
    type: String,
    required: true
  },
  alt: {
    type: String,
    default: ''
  },
  aspectRatio: {
    type: Number,
    default: 56.25 // 16:9 aspect ratio by default
  }
});

const loading = ref(true);
const error = ref(false);
const imageRef = ref(null);

const onImageLoad = () => {
  loading.value = false;
};

const onImageError = () => {
  loading.value = false;
  error.value = true;
};

// Initialize Intersection Observer only on client side
onMounted(() => {
  if (!process.client) return;

  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          const img = entry.target;
          img.src = img.dataset.src;
          observer.unobserve(img);
        }
      });
    },
    {
      rootMargin: '50px 0px',
      threshold: 0.01
    }
  );

  if (imageRef.value) {
    observer.observe(imageRef.value);
  }

  onUnmounted(() => {
    observer.disconnect();
  });
});
</script>