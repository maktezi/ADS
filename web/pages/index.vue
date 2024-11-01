<template>
  <main class="p-4 flex items-center justify-center">
<!--  PC/Tablet  -->
    <div v-if="!isMobile" class="p-0 md:p-2 xl:p-6 space-y-4 md:w-[800px] xl:w-[1400px]">
      <label class="text-3xl text-[#37474f] font-bold">{{ title }}</label>

      <div v-for="ad in ads" :key="ad.id" class="px-4 py-4 shadow-lg bg-white" >
        <div class="flex items-center justify-evenly gap-8">
          <div>
            <div class="title font-bold text-xl flex justify-center items-center">
              <img :src="ad.logo"  alt="logo" :class="ad.logoClass"/>
            </div>
            <div class="flex flex-col gap-3 w-full md:w-[300px] xl:w-[600px]">
              <div>
                {{ ad.details }}
              </div>
              <div class="text-[#266ba9]">
                {{ ad.details1 }}
              </div>
            </div>
          </div>

          <div class="flex md:flex-col xl:flex-row">
            <div class="p-2">
              <div v-for="i in ad.items" class="flex items-center">
                <div class="flex p-2 gap-2 items-center w-[180px]">
                  <div class="flex flex-col rounded-full bg-[#266ba9] p-2 items-center justify-center">
                    <Icon :name="i.icon" class="text-white" />
                  </div>

                  <div class="text-[#266ba9]">
                    {{ i.feature }}
                  </div>
                </div>

                <div class="md:w-[180px] xl:w[250px]">
                  {{ i.detail }}
                </div>
              </div>
            </div>

            <div class="flex flex-col md:items-start md:pl-4 xl:items-center justify-center space-y-2">
              <a :href="ad.website" target="_blank" class="bg-[#e64a19] text-white py-2 px-4 rounded-md flex items-center justify-center">
                <span>Visit website</span>
                <span><Icon name="ri:arrow-right-s-line" class="size-3" /></span>
              </a>

              <p class="underline text-gray-500 md:hidden xl:block">
                {{ ad.website }}
              </p>
            </div>

          </div>
        </div>
      </div>
    </div>

<!--  Mobile  -->
    <div v-else class="w-full py-4 px-6 text-center">
      <label class="text-3xl font-bold text-[#37474f]">{{ title }}</label>

      <div class="flex flex-col space-y-4 mt-4">
        <!-- Button Row -->
        <div class="flex justify-around">
          <button
              v-for="(ad, index) in ads"
              :key="ad.id"
              @click="toggleCard(index)"
              class="flex-1 px-4 py-2 h-[90px] flex items-center justify-center"
              :class="activeCard === index ? 'bg-white' : 'bg-gray-200'"
          >
            <img :src="ad.logoMobile" alt="logo" :class="ad.logoClassMobile" />
          </button>
        </div>

        <div v-if="activeCard !== null" class="flex flex-col gap-2 items-center bg-white p-4 shadow-md mt-2">
          <div class="text-[#37474f] text-xl font-bold">{{ ads[activeCard].name }}</div>
          <div class="mt-2">
            <ul class="list-disc list-inside">
              <li v-for="item in ads[activeCard].items" :key="item.feature" class="py-2 flex items-center">
                <div class="flex flex-col rounded-full bg-[#266ba9] p-2 items-center justify-center mr-2">
                  <Icon :name="item.icon" class="text-white" />
                </div>
                <span class="text-[#266ba9] mr-2">
                  {{ item.feature }}:
                </span>
                <span class="font-bold text-[#37474f]">
                  {{ item.detail }}
                </span>
              </li>
            </ul>
          </div>
          <a :href="ads[activeCard].website" target="_blank" class="bg-[#e64a19] text-white py-2 px-4 rounded flex items-center justify-center w-full py-4 mt-2 rounded-xl">
            <span>Visit website</span>
            <span><Icon name="ri:arrow-right-s-line" class="size-3" /></span>
          </a>
        </div>
      </div>
    </div>

    <Modal
      title="LIMITED TIME OFFER!"
      details="Save 82% On Private Internet Access. Offer Expires in:"
      discount="82% DISCOUNT ON VPN"
      stars="4.8 out of 5"
    />
  </main>
</template>

<script setup lang="ts">
import {ads, title} from '~/composables/constants'

const isMobile = inject('isMobile')

interface AdItem {
  id: string;
  logo: string;
  logoMobile: string;
  logoClass: string;
  logoClassMobile: string;
  details: string;
  details1: string;
  website: string;
  items: Array<{
    icon: string;
    feature: string;
    detail: string;
  }>;
}

defineProps<{
  title: string;
  ads: AdItem[];
  isMobile: boolean;
}>();

const activeCard = ref<number | null>(0);

const toggleCard = (index: number) => {
  activeCard.value = activeCard.value === index ? null : index;
};
</script>