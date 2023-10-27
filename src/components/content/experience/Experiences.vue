<script setup lang="ts">

import Experience from './Experience.vue';
import { WorkExperience } from './Experience.vue';
import RightArrow from '../../../assets/rightArrow.svg'
import ContentHeader from '../ContentHeader.vue';

const workExperiences: WorkExperience[] = [
    {
        startDate: "Jul '23'",
        endDate: "Now",
        company: "Nouveau Labs",
        title: "Software Engineer",
        description: "Integrated OAuth2.0 for Identity Provider login, improved API performance with asynchronous network calls, and enhanced data security through an S3 file URL system with 3-hour URL expiration. These efforts optimized user authentication, reduced execution times by 50%, and ensured data safety.",
        skills: ["Python", "Flask", "MySQL", "Elasticsearch", "Pytest"]
    },
    {
        startDate: "Jan '23",
        endDate: "Jun '23",
        company: "Amazon",
        title: "Software Development Engineer Intern",
        description: "Led the whole project from design to deployment. Migrated legacy backends to AWS, enriching them with robust features such as failure handling and reporting. Leveraged AWS Lambda for serverless solutions. Innovatively developed an API to streamline seamless backend communication. Demonstrated leadership through fostering collaboration and knowledge sharing within the engineering department.",
        skills: ["Java", "Typescript", "AWS Lambda", "Amazon S3", "Amazon DynamoDB", "Amazon SQS", "AWS IAM", "AWS ECS", "JUnit5"]
    },
    {
        startDate: "Dec '21",
        endDate: "Jul '22",
        company: "Atom.ei",
        title: "Android Developer Intern",
        description: "Collaborated with a talented team to develop a habit-building app. Implemented features such as app widgets, data caching, and data pre-fetching to enhance user experience and improve performance. By refactoring network calls, optimized app loading times, ensuring a smooth and efficient user interface, while actively contributing to the collaborative efforts of the team.",
        skills: ["Kotlin", "Java", "Android", "Firebase Firestore", "Firebase Cloud Messaging", "Widgets"]
    }
]
</script>

<template>
    <section id="experience" class="lg:mb-36 md:mb-24 mb-16 scroll-mt-24">
        <ContentHeader :text="'Experience'"/>
        <ul>
            <Experience v-for="work in workExperiences" :experience="work"/>
        </ul>
        <div class="mt-12">
            <a href="https://drive.google.com/file/d/1c3k_7Q5ZtW9ddV5GChbPwtERIN-aXguk/view?usp=sharing" target="_blank" class="inline-flex gap-1 items-center font-semibold leading-tight text-slate-200 group">
                <span class="border-b border-transparent py-px group-hover:border-teal-400 transition-all">View Full Résumé</span>
                <RightArrow class="group-hover:translate-x-2 transition-transform"/>
            </a>
        </div>
    </section>
</template>