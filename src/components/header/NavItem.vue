<script setup lang="ts">
import { computed } from 'vue';


export interface NavItemProps {
    readonly href: string
    readonly title: string
}

const props = defineProps<{
    navItem: NavItemProps,
    currentItem: NavItemProps
}>()

const isActive = computed(() => {
    return {
        active: (props.navItem.href === props.currentItem.href)
    }
})

</script>

<template>
    <li>
        <a class="py-3 items-center flex group" :class="isActive" :href="props.navItem.href">
            <span class="nav-indicator h-px w-8 mr-4 bg-slate-600 group-hover:bg-slate-200 group-hover:w-16 transition-all"/>
            <span class="nav-link text-xs font-bold uppercase tracking-widest group-hover:text-slate-200">
                {{ props.navItem.title }}
            </span>
        </a>
    </li>
</template>

<style scoped>

    .active .nav-indicator {
        --tw-bg-opacity: 1;
        background-color: rgb(226 232 240 / var(--tw-bg-opacity));
        width: 4rem;
    }

    .active .nav-link {
        --tw-text-opacity: 1;
        color: rgb(226 232 240 / var(--tw-text-opacity));
    }

</style>