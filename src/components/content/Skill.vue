<script setup lang="ts">

const props = defineProps<{
    skill: string
}>()

</script>

<template>
    <li>
        <div class="flex items-center rounded-full bg-teal-400/10 text-teal-300 px-3 py-1 text-xs font-medium leadin-5">
            {{ props.skill }}
        </div>
    </li>
</template>