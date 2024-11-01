<template>
  <div class="flex flex-col">
    <!-- Modal -->
    <div v-if="showModal" class="fixed inset-0 z-50 flex items-center justify-center bg-black/60">
      <div class="bg-white p-4 shadow-lg p-6 max-w-sm w-full">
        <button class="text-gray-500 float-right text-2xl" @click="closeModal">
          <Icon name="mdi:close" />
        </button>
        <div class="flex flex-col items-center justify-center w-full text-center mt-6">
          <div class="text-3xl font-bold animate-pulse">{{ title }}</div>
          <div class="text-sm">{{ details }}</div>

          <div class="text-5xl text-white p-2 flex flex-col w-full">
            <div class="flex justify-between px-4">
              <div class="text-black text-lg font-bold">Hours</div>
              <div class="text-black text-lg font-bold">Minutes</div>
              <div class="text-black text-lg font-bold">Seconds</div>
            </div>
            <div>
              <div class="flex justify-evenly">
                <div class="bg-black p-4 rounded">
                  <span class="font-bold">{{ formatTime(remainingTime).hours }}</span>
                </div>
                <span class="text-black mt-3">:</span>
                <div class="bg-black p-4 rounded">
                  <span class="font-bold">{{ formatTime(remainingTime).minutes }}</span>
                </div>
                <span class="text-black mt-3">:</span>
                <div class="bg-black p-4 rounded">
                  <span class="font-bold">{{ formatTime(remainingTime).seconds }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="flex items-center justify-center mt-4">
          <Icon v-for="i in 5" :key="i" name="mdi:star" class="text-white p-3 bg-green-400" />
          <div class="ml-2 text-sm">{{ stars }}</div>
        </div>


        <button class="mt-4 font-bold text-xl bg-red-500 w-full py-4 text-white py-2 px-4">
          {{ discount }}
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
defineProps({
  title: String,
  details: String,
  time: String,
  rating: Number,
  discount: String,
  stars: String
});

const showModal = ref(false);
const remainingTime = ref(86400);

const openModal = () => {
  showModal.value = true;
};

const closeModal = () => {
  showModal.value = false;
};

const formatTime = (seconds: number) => {
  const hours = Math.floor(seconds / 3600);
  const minutes = Math.floor((seconds % 3600) / 60);
  const secs = seconds % 60;
  return { hours: String(hours).padStart(2, '0'), minutes: String(minutes).padStart(2, '0'), seconds: String(secs).padStart(2, '0') };
};

let timer: NodeJS.Timeout;

onMounted(() => {
  timer = setInterval(() => {
    if (remainingTime.value > 0) {
      remainingTime.value--;
    } else {
      openModal();
      clearInterval(timer);
    }
  }, 1000);
});

onMounted(() => {
  setTimeout(() => {
    openModal()
  }, 5000)
})

onBeforeUnmount(() => {
  clearInterval(timer);
});
</script>
