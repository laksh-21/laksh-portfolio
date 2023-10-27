<script setup lang="ts">

import ContactItem, { ContactItemProps } from './ContactItem.vue';
import RightArrow from '../../../assets/rightArrow.svg'
import ContentHeader from '../ContentHeader.vue';
import { initializeApp } from "firebase/app";
import { collection, doc, getFirestore, setDoc, Timestamp } from "firebase/firestore";
import { computed, ref } from 'vue';

const name = ref("")
const email = ref("")
const content = ref("")
const nameError = ref(false)
const emailError = ref(false)
const contentError = ref(false)

const contactItems: ContactItemProps[] = [
    {
        itemId: "contact-name",
        label: "Your Name",
        placeholder: "Enter your name",
        rows: 1,
        binder: name,
        error: nameError
    },
    {
        itemId: "contact-email",
        label: "Email Address",
        placeholder: "Enter your email address",
        rows: 1,
        binder: email,
        error: emailError
    },
    {
        itemId: "contact-content",
        label: "Your Message",
        placeholder: "Hi, we need a developer for our product at Company X. How soon can you hop on to discuss this?",
        rows: 2,
        binder: content,
        error: contentError
    }
]

const firebaseConfig = {
  apiKey: "AIzaSyC0tweMnMXXnB9fYpHyPJusLrAte1QxaII",
  authDomain: "laksh-portfolio.firebaseapp.com",
  projectId: "laksh-portfolio",
  storageBucket: "laksh-portfolio.appspot.com",
  messagingSenderId: "486588574625",
  appId: "1:486588574625:web:6c491abd92b4b9bf90b9e0"
};

const app = initializeApp(firebaseConfig)
const db = getFirestore(app)

function isInputInvalid(): boolean {
    var nameInvalid = false
    var emailInvalid = false
    var contentInvalid = false

    nameError.value = (name.value.length === 0)
    nameInvalid = (name.value.length === 0)
    emailError.value = (email.value.length === 0 || email.value.indexOf('@') === -1)
    emailInvalid = (email.value.length === 0 || email.value.indexOf('@') === -1)
    contentError.value = (content.value.length === 0)
    contentInvalid = (content.value.length === 0)

    return nameInvalid || emailInvalid || contentInvalid
}

enum SubmitState {
    NONE = "NONE",
    FINISHED = "FINISHED",
    IN_PROGRESS = "IN_PROGRESS",
    ERROR = "ERROR"
}

const submitState = ref(SubmitState.NONE) 

async function submitResponse() {

    if (isInputInvalid()) {
        return
    }

    submitState.value = SubmitState.IN_PROGRESS

    const contactName = name.value
    const contactEmail = email.value
    const contactContent = content.value

    const newDocRef = doc(collection(db, "response"))
    
    setDoc(newDocRef, {
        name: contactName,
        email: contactEmail,
        content: contactContent,
        timestamp: Timestamp.now()
    }).then(() => {
        submitState.value = SubmitState.FINISHED

        name.value = ""
        nameError.value = false
        email.value = ""
        emailError.value = false
        content.value = ""
        contentError.value = false
    }).catch(() => {
        submitState.value = SubmitState.ERROR
        new Promise(r => setTimeout(r, 1000))
        .then(() => {
            submitState.value = SubmitState.NONE
        })
    })
}

const isButtonDisabled = computed(() => {
    return submitState.value === SubmitState.IN_PROGRESS || submitState.value === SubmitState.ERROR
})

const isProgressState = computed(() => {
    return submitState.value === SubmitState.IN_PROGRESS
})

const isErrorState = computed(() => {
    return submitState.value === SubmitState.ERROR
})

</script>

<template>
    <section id="contact" class="lg:mb-36 md:mb-24 mb-16 scroll-mt-24">
        <ContentHeader :text="'Contact'"/>
        <form name="contact" method="POST" data-netlify="true">
            <ul>
                <ContactItem v-for="contactItem in contactItems" :contact-item="contactItem"/>
            </ul>
        </form>
        <div class="mt-12 h-6">
            <a href="#" @click.prevent="submitResponse()" :class="{'hidden': isButtonDisabled}" class="inline-flex gap-1 items-center font-semibold leading-tight text-slate-200 group">
                <span class="border-b border-transparent py-px group-hover:border-teal-400 transition-all">Submit Response</span>
                <RightArrow class="group-hover:translate-x-2 transition-transform"/>
            </a>
            <div :class="{'hidden': !isProgressState}" class="inline-flex gap-2 items-center">
                <svg aria-hidden="true" class="w-6 h-6 text-gray-200 animate-spin dark:text-gray-600 fill-teal-500" viewBox="0 0 100 101" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z" fill="currentColor"/>
                    <path d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z" fill="currentFill"/>
                </svg>
                <p class="font-semibold leading-tight">Submitting Response</p>
            </div>
            <div :class="{'hidden': !isErrorState}" class="inline-flex gap-2 items-center">
                <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 stroke-red-400">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M11.25 11.25l.041-.02a.75.75 0 011.063.852l-.708 2.836a.75.75 0 001.063.853l.041-.021M21 12a9 9 0 11-18 0 9 9 0 0118 0zm-9-3.75h.008v.008H12V8.25z" />
                </svg>
                <p class="text-red-400 font-semibold leading-tight">Please Try Again</p>
            </div>
        </div>
    </section>
</template>