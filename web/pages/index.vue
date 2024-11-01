<template>
  <main class="p-4 flex items-center justify-center">
    <div class="p-0 md:p-2 xl:p-6 space-y-4 md:w-[800px] xl:w-[1400px]" v-if="!isMobile">
      <label class="text-3xl font-bold">
        Compare Our Top 3 VPNs
      </label>

      <div v-for="ad in ads" :key="ad.logo" class="px-4 py-4 shadow-xl" >
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
              <a :href="`https:\\${ad.website}`" target="_blank" class="bg-[#e64a19] text-white py-2 px-4 rounded-md flex items-center justify-center">
                <span>Visit Website</span>
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
  </main>
</template>

<script setup lang="ts">
import { ads } from '~/composables/constants'

const isMobile = inject('isMobile')
</script>