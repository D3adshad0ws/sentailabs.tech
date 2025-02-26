<script setup lang="ts">
const { data: page } = await useAsyncData('home', () => {
  return queryCollection('content').first()
})

useSeoMeta({
  title: page.value.title,
  ogTitle: page.value.title,
  description: page.value.description,
  ogDescription: page.value.description
})

const isDark = computed(() => useColorMode().value == 'dark')
</script>

<template>
  <div class="relative">
    <UPageHero
      :title="page.hero.title"
      :description="page.hero.description"
      :links="page.hero.links"
      class="relative"
    >
      <template #top>
        <div class="absolute rounded-full dark:bg-(--ui-primary) blur-[300px] size-60 sm:size-80 transform -translate-x-1/2 left-1/2 -translate-y-80" />

        <ParticlesBg
          class="absolute inset-0 z-[-1] h-[400px]"
          :quantity="100"
          :ease="100"
          :color="isDark ? '#FFF' : '#000'"
          :staticity="10"
          refresh
        />
      </template>
    </UPageHero>

    <StarsBg />
    <UPageSection
      id="features"
      v-bind="page.templates"
      class="overflow-hidden"
    >
      <UCarousel
        v-slot="{ item }"
        loop
        arrows
        dots
        :autoplay="{ delay: 5000 }"
        :items="page.templates.items"
        :ui="{ item: 'basis-1/2', container: 'py-2' }"
      >
        <UPageCard
          :to="item.to"
          :description="item.description"
          class="group"
          :ui="{ container: 'p-4 sm:p-4', title: 'flex items-center gap-1' }"
        >
          <template #title>
            <UIcon :name="item.icon" />
            <span>
              {{ item.title }}
            </span>
          </template>
          <img
            :src="item.image"
            :alt="item.title"
            class="rounded-lg grayscale group-hover:grayscale-0 transition-all duration-200 ease-in-out"
          >
        </UPageCard>
      </UCarousel>
    </UPageSection>
    <UPageSection>
      <UPageMarquee
        pause-on-hover
        class="[--duration:50s]"
      >
        <img
          v-for="(logo, index) in page.logos"
          :key="index"
          v-bind="logo"
          class="h-6 shrink-0 max-w-[140px] filter invert dark:invert-0"
        >
      </UPageMarquee>
    </UPageSection>

    <LazyUPageSection />

    <UPageSection
      id="faq"
      v-bind="page.faq"
      class="scroll-mt-(--ui-header-height)"
    >
      <UPageAccordion
        multiple
        :items="page.faq.items"
        class="max-w-4xl mx-auto"
      >
        <template #body="{ item }">
          <MDC
            :value="item.content"
            unwrap="p"
          />
        </template>
      </UPageAccordion>
    </UPageSection>

    <USeparator />
    <UPageCTA
      v-bind="page.cta"
      variant="naked"
      class="overflow-hidden"
    >
      <ParticlesBg
        class="absolute inset-0 z-[-1] h-[400px]"
        :quantity="300"
        :ease="100"
        :color="isDark ? '#FFF' : '#000'"
        :staticity="10"
      />
      <div class="absolute rounded-full dark:bg-(--ui-primary) blur-[250px] size-40 sm:size-50 transform -translate-x-1/2 left-1/2 -translate-y-80" />
    </UPageCTA>
  </div>
</template>
