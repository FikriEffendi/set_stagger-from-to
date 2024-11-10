<template>
  <div class="flex items-center justify-center h-screen gap-32">
    <template v-for="(image, index) in images" :key="index">
      <div class="relative">
        <div class="aspect-[9/16] w-72">
          <img
            :src="image.src"
            class="object-cover w-full h-full"
            :alt="image.alt"
            ref="imageRefs"
          />
        </div>
        <div
          class="absolute inset-0 flex items-center justify-center text-2xl font-bold text"
          :class="image.textClass"
        >
          <div>{{ image.text }}</div>
        </div>
      </div>
    </template>
  </div>
</template>

<script setup>
import gsap from "gsap";
import { onMounted, ref } from "vue";

const images = [
  {
    src: "../../public/img1.jpg",
    alt: "",
    text: "Living",
    textClass: "text-white",
  },
  {
    src: "../../public/img2.jpg",
    alt: "",
    text: "In",
    textClass: "text-white",
  },
  {
    src: "../../public/img3.jpg",
    alt: "",
    text: "Abstraction",
    textClass: "text-[#6cb8d1] underline",
  },
];

const imageRefs = ref([]);

onMounted(() => {
  gsap.set(imageRefs.value, {
    yPercent: -115,
  });

  gsap.set(".text", {
    opacity: 0,
  });

  gsap.to(imageRefs.value, {
    yPercent: 0,
    scale: 1.12,
    delay: 0.5,
    duration: 1.5, //durasi keseluruhan animasi sampai semua gambar keluar
    stagger: 0.1,
    ease: "power4.out",
    onComplete: scaleDownAndFadeIn,
  });
});

const scaleDownAndFadeIn = () => {
  gsap.to(imageRefs.value, {
    scale: 1,
    duration: 1,
  });
};
</script>

<style lang="scss" scoped></style>
