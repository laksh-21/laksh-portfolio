<script setup lang="ts">
import Introduction from './introduction/Introduction.vue';
import Experiences from './experience/Experiences.vue';
import Projects from './projectsMade/Projects.vue';
import Contact from './contact/Contact.vue';
import Footer from './footer/Footer.vue';
</script>

<template>
    <main class="py-24 lg:w-1/2">
        <Introduction/>
        <Experiences/>
        <Projects/>
        <Contact/>
        <Footer/>
    </main>
</template>