<script setup lang="ts" name="AboutSection">
import { Linear, gsap } from 'gsap'
import { ScrollTrigger } from 'gsap/dist/ScrollTrigger'

const quoteRef: Ref<HTMLElement | undefined> = ref(undefined)
const targetSection: Ref<HTMLElement | undefined> = ref(undefined)

const willChange = ref(false)

function initAboutAnimation(quoteRef: Ref<HTMLElement | undefined>, targetSection: Ref<HTMLElement | undefined>): ScrollTrigger {
  
  const timeline = gsap.timeline({
    defaults: { ease: Linear.easeNone, duration: 0.1 },
  })
  timeline
    .fromTo(quoteRef.value!.querySelector('.about-1'), { opacity: 0.2 }, { opacity: 1 })
    .to(quoteRef.value!.querySelector('.about-1'), {
      opacity: 0.2,
      delay: 0.5,
    })
    .fromTo(quoteRef.value!.querySelector('.about-2'), { opacity: 0.2 }, { opacity: 1 }, '<')
    .to(quoteRef.value!.querySelector('.about-2'), {
      opacity: 0.2,
      delay: 1,
    })

  const scrollTriggerInstance = ScrollTrigger.create({
    trigger: targetSection.value,
    start: 'center 80%',
    end: 'center top',
    scrub: 0,
    animation: timeline,
    onToggle: self => willChange.value = self.isActive,
  })
  return scrollTriggerInstance
}

onMounted(() => {
  const aboutScrollTriggerInstance = initAboutAnimation(quoteRef, targetSection)
  return aboutScrollTriggerInstance.kill
})
</script>

<template>
  <section ref="targetSection" class="section-container relative w-full select-none pb-16 ">
    <div class="pb-2 text-lg ">
      <!-- <p>生活是这样吗？？？</p> -->
      <p>{{"while(true){"}}</p>
      <p class="pl-2">{{"eat()"}}</p>
      <p class="pl-2">{{'sleep()'}}</p>
      <p class="pl-2">{{'write_code()'}}</p>
      <p>{{"}"}}</p>
    </div>
    <h1 ref="quoteRef" class="text-3xl font-medium md:text-6xl sm:text-4xl">
      <span :class="`about-1 leading-tight ${willChange ? 'will-change-opacity' : ''}`">
        我们要飞向何方。我打算待会去码头整点薯条；
         <!-- 人这一生不过是把短短的赶路人,路漫漫其修远兮,惟有执着追求理想和梦想,才能在平庸的生命历程中留下闪亮的足迹,绽放出生命的绚丽光芒。 -->
      </span>
      <span :class="`about-2 leading-tight ${willChange ? 'will-change-opacity' : ''}`">
      宇宙的尽头是什么。  “薯条”
      </span>
    </h1>
  </section>
</template>
