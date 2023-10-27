<script setup lang="ts">

import Link from '../../../assets/link.svg'

export interface LinkProps {
    href: string,
    text: string
}

const props = defineProps<LinkProps>()

</script>

<template>
    <a :href="props.href" class="transition-all inline-flex gap-1 items-center text-sm font-medium text-slate-300 hover:text-teal-300" target="_blank">
        <Link/>
        <span>
            {{ props.text }}
        </span>
    </a>
</template>