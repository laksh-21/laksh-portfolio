<script setup lang="ts">
import Profile from './Profile.vue'
import Navigation from './Navigation.vue';
import Socials from './Socials.vue';
</script>

<template>
    <header class="lg:py-24 lg:sticky top-0 md:w-1/2 lg:max-h-screen lg:flex lg:flex-col justify-between">
        <div>
            <Profile/>
            <Navigation/>
        </div>
        <Socials/>
    </header>
</template>