<script setup lang="ts">
    const props = defineProps<{
        text: string
    }>()
</script>

<template>
    <div class="sticky top-0 z-20 w-full mb-4 bg-slate-900/75 py-5 backdrop-blur lg:sr-only lg:relative lg:top-auto lg:mx-auto lg:w-full lg:py-0 lg:opacity-0">
            <h2 class="text-sm font-bold uppercase tracking-widest text-slate-200 lg:sr-only">
                {{ props.text }} 
            </h2>
        </div>
</template>