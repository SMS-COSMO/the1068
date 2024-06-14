<template>
  <!-- Preload fonts -->
  <span v-for="f in boskaFamily" :key="f" :style="`font-family: ${f}`" />
  <div
    class="-z-10 -top-[400px] -right-[300px] h-[1000px] w-[1000px] fixed blur-[400px] rounded-full opacity-20 transition-all duration-500"
    :style="selected === 'fm'
      ? 'background-color: #1185D6'
      : 'background-color: #EB5228'"
  />
  <div class="h-screen w-screen md:flex gap-20 pt-20 md:pt-0 px-8 md:px-10 lg:px-24">
    <div class="self-center flex basis-3/5 md:mt-10 justify-center md:justify-end select-none leading-tight">
      <div class="transition-all duration-500 text-6xl md:text-[8vw] h-fit">
        <span :style="`font-family: ${font1}`">the</span>
        <span :style="`font-family: ${font2}`">1068.</span>
      </div>
      <div>
        <div
          class="transition-all duration-500 cursor-pointer"
          :style="selected === 'guide' && `transform: translateY(-${guideHeight}px)`"
        >
          <div
            class="clash-bold fm-gradient w-fit text-6xl md:text-[8vw] transition-all duration-500"
            :class="[selected === 'fm' ? 'opacity-100' : 'opacity-40 hover:opacity-80']"
            :style="selected === 'fm' && 'text-shadow: 0 0 1em #086FDFB0'"
            @mousedown="selected = 'fm'"
          >
            fm
          </div>
          <div
            ref="guide"
            class="clash-bold guide-gradient text-6xl md:text-[7vw] transition-all duration-500"
            :class="[selected === 'guide' ? 'opacity-100' : 'opacity-40 hover:opacity-80']"
            :style="selected === 'guide' && 'text-shadow: 0 0 1em #EB7428B0'"
            @mousedown="selected = 'guide'"
          >
            guide
          </div>
        </div>
      </div>
    </div>
    <div class="shadow-white self-center basis-2/5 mt-16 md:mt-0">
      <Transition name="slide-up" mode="out-in">
        <div v-if="selected === 'fm'" style="text-shadow: 0 0 4em #FFFFFF50" class="text-center md:text-start">
          <h1 class="scroll-m-20 text-4xl md:text-5xl font-extrabold tracking-tight">
            风华子衿广播站点歌系统
          </h1>
          <p class="leading-relaxed md:text-xl [&:not(:first-child)]:mt-6">
            the1068fm 是由 COSMO 智慧校园平台运研中心为风华子衿广播站<b>声声慢</b>点歌节目开发的一体化系统，包含歌曲投稿，歌曲审核，一键排歌，导出歌单等功能。
          </p>
          <div class="mt-8 flex gap-4 justify-center md:justify-start">
            <NuxtLink to="https://fm.the1068.pictures/">
              <Button>
                访问
                <Icon name="lucide:arrow-up-right" class="ml-2" />
              </Button>
            </NuxtLink>
            <NuxtLink to="https://github.com/SMS-COSMO/the1068fm">
              <Button size="icon" variant="outline">
                <Icon name="lucide:github" size="16" />
              </Button>
            </NuxtLink>
          </div>
        </div>
        <div v-else style="text-shadow: 0 0 4em #FFFFFF50" class="text-center md:text-start">
          <h1 class="scroll-m-20 text-4xl md:text-5xl font-extrabold tracking-tight">
            深中漫游指南
          </h1>
          <p class="leading-relaxed md:text-xl [&:not(:first-child)]:mt-6">
            一份 不太常规的 深中漫游指南。
          </p>
          <div class="mt-8 flex gap-4 justify-center md:justify-start">
            <NuxtLink to="https://guide.the1068.pictures/">
              <Button>
                访问
                <Icon name="lucide:arrow-up-right" class="ml-2" />
              </Button>
            </NuxtLink>
            <NuxtLink to="https://github.com/SMS-COSMO/the1068guide">
              <Button size="icon" variant="outline">
                <Icon name="lucide:github" size="16" />
              </Button>
            </NuxtLink>
          </div>
        </div>
      </Transition>
    </div>
  </div>
  <footer class="fixed bottom-4 w-screen flex flex-col md:flex-row md:opacity-0 md:hover:opacity-50 pt-40 px-10 transition-all duration-500">
    <span class="self-center" style="font-family: Boska-Regular;">
      the1068.pictures
    </span>
    <span class="md:ml-auto self-center" style="font-family: Boska-Bold;">
      Designed By COSMO.
    </span>
    <NuxtLink class="md:ml-auto self-center" to="https://github.com/SMS-COSMO/the1068">
      <Button size="icon" variant="ghost">
        <Icon name="lucide:github" size="16" />
      </Button>
    </NuxtLink>
  </footer>
</template>

<script setup lang="ts">
definePageMeta({
  colorMode: 'dark',
});

const selected = ref<'fm' | 'guide'>('fm');
const guide = ref();
const { height: guideHeight } = useElementSize(guide);

const boskaFamily = [
  'Boska-Extralight',
  'Boska-ExtralightItalic',
  'Boska-Light',
  'Boska-LightItalic',
  'Boska-Regular',
  'Boska-Italic',
  'Boska-Medium',
  'Boska-MediumItalic',
  'Boska-Bold',
  'Boska-BoldItalic',
  'Boska-Black',
  'Boska-BlackItalic',
];
const font1 = ref('Boska-Bold');
const font2 = ref('Boska-BoldItalic');

useIntervalFn(() => {
  font1.value = boskaFamily[Math.floor(Math.random() * boskaFamily.length)];
  font2.value = boskaFamily[Math.floor(Math.random() * boskaFamily.length)];
}, 1500);
</script>

<style scoped>
.clash-bold {
  font-family: ClashDisplay-Bold;
}

.fm-gradient {
  background: linear-gradient(120.841deg, #086FDF 0%, #1185D6 26%, #24B5C3 50%, #0BCF7D 74%, #3DF5A7 100%);
  color: transparent;
  background-clip: text;
  -webkit-background-clip: text;
}

.guide-gradient {
  background: linear-gradient(120.841deg, #EB2881 0%, #EB3028 30%, #EB5228 54%, #EB7428 79%, #EB9628 100%);
  color: transparent;
  background-clip: text;
  -webkit-background-clip: text;
}

.slide-up-enter-active,
.slide-up-leave-active {
  transition: all 0.2s ease-in-out;
}

.slide-up-enter-from,
.slide-up-leave-to {
  opacity: 0;
}
</style>
