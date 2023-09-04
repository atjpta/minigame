<template>
  <div>
    <div class="container p-10 mx-auto">
      <div class="relative w-[700px] h-60 mx-auto">
        <div class="absolute inset-y-5 inset-x-[49.5%] bg-red-500 z-50"></div>
        <div ref="carousel" :class="isScroll ? '' : 'overflow-x-hidden'"
          class="w-full h-full scroll-smooth carousel carousel-center rounded-box">
          <TransitionGroup name="list">
            <div class="carousel-item overflow-hidden mx-[25px]" v-for="i in list" :key="i.id">
              <img :src="i.url" />
            </div>
          </TransitionGroup>
        </div>
      </div>
      <div class="flex justify-center m-5">
        <div @click="scrolling()" :class="loading ? 'loading' : ''" class="btn">
          scroll
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, onUpdated, ref } from "vue";
const list = ref([]);
const loading = ref(false);
const isScroll = ref(true);
const index = ref(2);
const delay = 500;
const carousel = ref();
const listDefault = [
  { id: 1, url: "https://daisyui.com/images/stock/photo-1559703248-dcaaec9fab78.jpg" },
  { id: 2, url: "https://daisyui.com/images/stock/photo-1565098772267-60af42b81ef2.jpg" },
  { id: 3, url: "https://daisyui.com/images/stock/photo-1572635148818-ef6fd45eb394.jpg" },
  { id: 4, url: "https://daisyui.com/images/stock/photo-1559703248-dcaaec9fab78.jpg" },
  { id: 5, url: "https://daisyui.com/images/stock/photo-1565098772267-60af42b81ef2.jpg" },
  { id: 6, url: "https://daisyui.com/images/stock/photo-1572635148818-ef6fd45eb394.jpg" },
  { id: 7, url: "https://daisyui.com/images/stock/photo-1559703248-dcaaec9fab78.jpg" },
  { id: 8, url: "https://daisyui.com/images/stock/photo-1565098772267-60af42b81ef2.jpg" },
  { id: 9, url: "https://daisyui.com/images/stock/photo-1572635148818-ef6fd45eb394.jpg" },
  { id: 10, url: "https://daisyui.com/images/stock/photo-1559703248-dcaaec9fab78.jpg" },
  {
    id: 11,
    url: "https://daisyui.com/images/stock/photo-1565098772267-60af42b81ef2.jpg",
  },
  {
    id: 12,
    url: "https://daisyui.com/images/stock/photo-1572635148818-ef6fd45eb394.jpg",
  },
  { id: 13, url: "https://daisyui.com/images/stock/photo-1559703248-dcaaec9fab78.jpg" },
  {
    id: 14,
    url: "https://daisyui.com/images/stock/photo-1565098772267-60af42b81ef2.jpg",
  },
  {
    id: 15,
    url: "https://daisyui.com/images/stock/photo-1572635148818-ef6fd45eb394.jpg",
  },
  { id: 16, url: "https://daisyui.com/images/stock/photo-1559703248-dcaaec9fab78.jpg" },
  {
    id: 17,
    url: "https://daisyui.com/images/stock/photo-1565098772267-60af42b81ef2.jpg",
  },
  {
    id: 18,
    url: "https://daisyui.com/images/stock/photo-1572635148818-ef6fd45eb394.jpg",
  },
  { id: 19, url: "https://daisyui.com/images/stock/photo-1559703248-dcaaec9fab78.jpg" },
  {
    id: 20,
    url: "https://daisyui.com/images/stock/photo-1565098772267-60af42b81ef2.jpg",
  },
];

const createData = (size) => {
  for (let i = 0; i < size; i++) {
    list.value.push(listDefault[i]);
  }
};

const scrolling = () => {
  loading.value = true;
  let random = ~~(Math.random() * 100) % 20;
  if (random < 5) {
    random = 5;
  }
  let times = 0;
  list.length = 0;
  const scroll = setInterval(() => {
    times++;
    if (times >= random) {
      clearInterval(scroll);
      loading.value = false;
    }
    index.value++;
    if (index.value == listDefault.length) {
      index.value = 0;
    }
    list.value.shift();
    setTimeout(() => {
      list.value.push(listDefault[index.value]);
    }, delay / 2);
  }, delay);
};

onMounted(() => {
  createData(3);
});
</script>

<style>
.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.2s ease;
}

.list-leave-active {
  opacity: 0;
  display: none;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(-30px);
}
</style>
