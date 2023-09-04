<template>
  <div>
    <div class="flex justify-center space-x-5">
      <scroll @start="start" @finish="finish" :id="0" :start="isStart" />
      <scroll @start="start" @finish="finish" :id="1" :start="isStart" />
      <scroll @start="start" @finish="finish" :id="2" :start="isStart" />
    </div>
    <div class="text-center m-5">
      {{ resultAll }}
    </div>
    <div class="flex justify-center m-5">
      <div @click="scrolling()" :class="isLoading ? 'loading' : ''" class="btn">
        start
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed, onMounted, ref, watch } from "vue";
import scroll from "./components/scroll3.vue";
const loading = ref([false, false, false]);
const resultAll = ref([]);
const isLoading = computed(() => {
  let result = false;
  loading.value.forEach((e) => {
    if (e) {
      result = true;
      return;
    }
  });
  return result;
});

const isStart = ref(false);
const scrolling = () => {
  resultAll.value.length = 0;
  isStart.value = true;
};

const finish = (i, result) => {
  loading.value[i] = false;
  resultAll.value[i] = result;
};

const start = (i) => {
  loading.value[i] = true;
};

watch(isLoading, () => {
  if (!isLoading.value) {
    isStart.value = false;
  }
});
</script>

<style></style>
