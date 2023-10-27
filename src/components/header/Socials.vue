<script setup lang="ts">

import SocialItem, { SocialProps } from './SocialItem.vue';

const socialItems: SocialProps[] = [
    {
        href: "https://www.linkedin.com/in/laksh-21/",
        websiteName: "LinkedIn"
    },
    {
        href: "https://github.com/laksh-21",
        websiteName: "Github"
    },
    {
        href: "mailto: laksh.ch21@gmail.com",
        websiteName: "Gmail"
    },
]

</script>

<template>
    <ul class="mt-8 flex gap-4 items-center">
        <SocialItem v-for="socialItem in socialItems" :href="socialItem.href" :website-name="socialItem.websiteName"/>
    </ul>
</template>