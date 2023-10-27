<script setup lang="ts">
import { ProjectProps } from './Project.vue';
import Project from './Project.vue';
import ContentHeader from '../ContentHeader.vue';


const projects: ProjectProps[] = [
    {
        projectName: "Protext",
        projectDescription: "A versatile app that combines the functionality of a bookmark manager and a text copying utility. Efficiently organize bookmarks into folders for easy access and streamline the process of copying large sections of text.",
        skills: ["Kotlin", "Android", "Room SQLite", "Multi module"],
        imgLink: "/protext.png",
        links: [
            {
                href: "https://play.google.com/store/apps/details?id=better.text.protext&hl=en-IN",
                text: "Play Store"
            },
            {
                href: "https://github.com/laksh-21/ProText",
                text: "Github"
            }
        ]
    },
    {
        projectName: "ChAes",
        projectDescription: "A dynamic chat application built on Google Firebase, featuring essential functionalities like unread message count, user authentication, and user search.",
        skills: ["Kotlin", "Android", "Firebase Firestore", "Jetpack Compose"],
        imgLink: "/ChAes.png",
        links: [
            {
                href: "https://github.com/laksh-21/ChAES",
                text: "Github"
            }
        ]
    }
]

</script>

<template>
    <section class="lg:mb-36 md:mb-24 mb-16 scroll-mt-24" id="projects">
        <ContentHeader :text="'Projects'"/>
        <ul>
            <Project v-for="project in projects" :project="project"/>
        </ul>
    </section>
</template>