
<template>
  <div class="section slogan">
    這台相機，最懂拍出你的型。
  </div>
  <div
    class="section section2"
    :class="{ sticky: fixClass }"
  >
    <div
      class="section bgR"
      :class="{ static: fixClass }"
    >
    </div>
    <div
      class="section bgG"
      :class="{ static: fixClass }"
    >
    </div>
    <div
      class="section bgB"
      :class="{ static: fixClass }"
    >
    </div>
  </div>
  <div
    class="section bgG"
    :class="{ static: fixClass }"
  >
  </div>
  <div
    class="section bgB"
    :class="{ static: fixClass }"
  >
  </div>
  <div class="section slogan">
    這台相機，最懂拍出你的型。
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue'

const progress = ref(0)

/**
 * progress : 3 ~ 1
 * progress 代表 css scale 的值
 */
onMounted(() => {
  const app = document.querySelector('#app')
  const section = document.querySelector('.section2')
  app.addEventListener('scroll', function (e) {
    // scrollTop 還在第 1 個區塊 (section1) 之間，progress 不變
    if (app.scrollTop < window.innerHeight) {
      progress.value = 0
    }
    // scrollTop 超過第 3 個區塊 ( section3)，progress 等於 1
    else if (app.scrollTop > window.innerHeight * 3) {
      progress.value = 1
    }
    // scrollTop 在第 2 ~ 3 個區塊，progress 變化
    else {
      // progress
      progress.value = Math.round(((app.scrollTop - window.innerHeight) / (window.innerHeight * 2)) * 100) / 100
    }
    let position = (section.scrollWidth - window.innerWidth) * progress.value
    section.scrollTo({ left: position })

    console.log(section.scrollWidth)
    console.log(progress.value)
  })
})

// 當卷軸進程還還在 section2 以上，也就是要讓 scale 變動的區間
const fixClass = computed(() => {
  return progress.value < 1
})

</script>

<style lang="sass">
  @import '@/style/app.sass'
  

</style>
