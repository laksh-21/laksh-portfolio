<script setup lang="ts">

import Skill from '../Skill.vue'
import Link from './Link.vue'
import { LinkProps } from './Link.vue'

export interface ProjectProps {
    readonly projectName: string
    readonly projectDescription: string
    readonly skills: string[]
    readonly imgLink: string
    readonly links: LinkProps[]
}

const props = defineProps<{
    project: ProjectProps
}>()

</script>

<template>
    <li class="mb-12">
        <div class="grid sm:grid-cols-8 sm:gap-4">
            <div class="col-span-6 sm:order-2">
                <h3 class="font-medium leading-tight text-slate-200">
                    {{ props.project.projectName }}
                </h3>
                <p class="mt-2 leading-normal text-sm">{{ props.project.projectDescription }}</p>
                <ul class="mt-4 flex flex-wrap gap-2">
                    <Link v-for="link in props.project.links" :href="link.href" :text="link.text"/>
                </ul>
                <ul class="mt-4 mb-4 sm:mb-0 flex flex-wrap gap-2">
                    <Skill v-for="skill in props.project.skills" :skill="skill"/>
                </ul>
            </div>
            <img loading="lazy" :src="props.project.imgLink" width="200" height="48" class="sm:order-1 col-span-2 rounded border-2 border-slate-200/10"/>
        </div>
    </li>
</template>