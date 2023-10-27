<script setup lang="ts">
import { Ref, computed } from 'vue'


export interface ContactItemProps {
    readonly itemId: string
    readonly label: string
    readonly placeholder: string
    readonly rows: number
    readonly binder: Ref
    readonly error: Ref
}

const props = defineProps<{
    contactItem: ContactItemProps
}>()

const outlineColors = computed(() => ({
    'border-gray-600': !props.contactItem.error.value,
    'border-red-500': props.contactItem.error.value,
    'focus:border-teal-500': !props.contactItem.error.value,
    'focus:border-red-500': props.contactItem.error.value
}))

</script>

<template>
    <li class="mb-12">
        <div class="grid sm:grid-cols-8 sm:gap-4 items-end">
            <label for="contact_name" class="font-semibold text-s tracking-wide col-span-2 focus:text-teal-400">
                {{ props.contactItem.label }}
            </label>
            <div class="col-span-6">
                <textarea v-model="props.contactItem.binder.value" :id="props.contactItem.itemId" :rows="props.contactItem.rows" :placeholder="props.contactItem.placeholder" :class="outlineColors" class="resize-none font-light transition-all w-full bg-transparent text-slate-300 border-b outline-none py-2.5 br-1.5"/>
            </div>
        </div>
    </li>
</template>