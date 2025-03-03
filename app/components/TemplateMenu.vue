<template>
  <UDropdownMenu
    v-slot="{ open }"
    :modal="false"
    :items="[{
      label: `Portal`,
      to: 'https://example.com'
    }, {
      label: `Sentai`,
      to: '',
      color: 'primary',
      checked: true,
      type: 'checkbox'
    }, {
      label: `About`,
      to: 'https://example.com'
    }, {
      label: `Contact`,
      to: 'https://example.com'
    }, {
      label: `Login`,
      to: 'https://example.com'
    }]"
    :ui="{ content: 'w-(--reka-dropdown-menu-trigger-width) min-w-0' }"
    size="xs"
  >
    <UButton
      label="Sentai"
      variant="subtle"
      trailing-icon="i-lucide-chevron-down"
      size="xs"
      class="-mb-[6px] font-semibold rounded-full truncate"
      :class="[open && 'bg-(--ui-primary)/15']"
      :ui="{
        trailingIcon: ['transition-transform duration-200', open ? 'rotate-180' : undefined].filter(Boolean).join(' ')
      }"
    />
  </UDropdownMenu>
</template>
