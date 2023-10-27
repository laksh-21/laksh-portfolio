<script setup lang="ts">
import LinkedIn from '../../assets/linkedin.svg'
import Github from '../../assets/github.svg'
import Gmail from '../../assets/gmail.svg'

export interface SocialProps {
    readonly href: string,
    readonly websiteName: string
}
const props = defineProps<SocialProps>()

function getWebsite() {
    if (props.websiteName === 'Github') {
        return Github
    } else if (props.websiteName === 'LinkedIn') {
        return LinkedIn
    } else {
        return Gmail
    }
}

</script>

<template>
    <li>
        <a :href="props.href" class="hover:text-slate-200" target="_blank">
            <span class="sr-only">{{ props.websiteName }}</span>
            <component :is="getWebsite()"/>
        </a>
    </li>
</template>