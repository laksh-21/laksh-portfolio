<script setup lang="ts">
import { NavItemProps } from './NavItem.vue';
import NavItem from './NavItem.vue';
import { onMounted, onUnmounted, ref } from 'vue';

const navItems: NavItemProps[] = [
    {
        href: "#intro",
        title: "Introduction",
    },
    {
        href: "#experience",
        title: "Experience"
    },
    {
        href: "#projects",
        title: "Projects"
    },
    {
        href: "#contact",
        title: "Contact"
    },
]

const currentItem = ref(navItems[0])

function updateCurrentItem(navItem: NavItemProps) {
    currentItem.value = navItem
}

var sections: NodeListOf<HTMLElement>

onMounted(() => {
    sections = document.querySelectorAll("section")
    window.addEventListener('scroll', handleScroll, false)
})

onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll)
})

function handleScroll() {
    sections.forEach((section) => {
        const sectionTop = section.offsetTop
        if (scrollY >= sectionTop - (section.offsetHeight / 2)) {
            const sectionId = section.getAttribute("id")
            const navItemIndex = navItems.findIndex((item) => item.href === (`#${sectionId}`))
            updateCurrentItem(navItems[navItemIndex])
        }
    })
}

</script>

<template>
    <nav class="hidden lg:block">
        <ul class="mt-16 w-max">
            <NavItem v-for="navItem in navItems" :nav-item="navItem" :current-item="currentItem" @click="updateCurrentItem(navItem)"/>
        </ul>
    </nav>
</template>