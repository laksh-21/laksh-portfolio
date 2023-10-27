<script setup lang="ts">

import Skill from '../Skill.vue'

export interface WorkExperience {
    readonly startDate: string
    readonly endDate: string
    readonly company: string
    readonly title: string
    readonly description: string
    readonly skills: string[]
}

const props = defineProps<{
    experience: WorkExperience
}>()

</script>

<template>
    <li class="mb-12">
        <div class="grid sm:grid-cols-8 sm:gap-4">
            <header class="mt-1 mb-2 sm:mb-0 uppercase font-semibold text-xs tracking-wide col-span-2">
                {{ props.experience.startDate }} — {{ props.experience.endDate }}
            </header>
            <div class="col-span-6">
                <h3 class="font-medium text-slate-200">
                    {{ props.experience.title }} · {{ props.experience.company }}
                </h3>
                <p class="mt-2 text-sm leading-normal">
                    {{ props.experience.description }}
                </p>
                <ul class="mt-2 flex flex-wrap gap-2">
                    <Skill v-for="skill in props.experience.skills" :skill="skill"/>
                </ul>
            </div>
        </div>
    </li>
</template>