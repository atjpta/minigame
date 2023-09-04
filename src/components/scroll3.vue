<template>
    <div>
        <div class="container p-10 mx-auto"></div>
        <div class="h-[350px] overflow-hidden w-fit mx-auto rounded-box ring-4">
            <transition-group name="list">
                <div v-for="i in list" :key="i"
                    class="h-[200px] w-[200px] -translate-y-[125px] text-9xl flex justify-center items-center">
                    {{ i }}
                </div>
            </transition-group>
        </div>
    </div>
</template>

<script setup>
import { onMounted, defineProps, ref, watch } from "vue";

const props = defineProps({
    start: Boolean,
    id: Number,
});

const list = ref([]);

const isScroll = ref(true);
const index = ref(2);
const delay = 500;
const listDefault = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
listDefault.length = 10;
const createData = (size) => {
    for (let i = 0; i < size; i++) {
        list.value.push(listDefault[i]);
    }
};

const scrolling = () => {
    let random = ~~(Math.random() * 100) % 20;
    if (random < 2) {
        random = 1;
    }
    let times = 0;
    list.length = 0;
    const scroll = setInterval(() => {
        times++;
        if (times >= random) {
            clearInterval(scroll);
            finish();
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

const emit = defineEmits(["finish", "start"]);
const finish = () => {
    emit("finish", props.id, listDefault[index.value]);
};
const start = () => {
    emit("start", props.id);
};

watch(props, () => {
    if (props.start) {
        start();
        scrolling();
    }
});

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
