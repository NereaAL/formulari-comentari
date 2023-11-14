<template>
    <h2>Formulari</h2>
    <form @submit.prevent="gestionarSubmit">
        <textarea :value="body"
        @keyup="recollirTextForm"
        name="" id="" cols="50" rows="10"></textarea>
        <br>
        <span>{{ charCount }} / {{maxCaracters}}</span>
        <Emoticonos v-model="emoji"></Emoticonos>
        <!-- <div v-if="">
            <p>Has superat els caracters permesos</p>
        </div> -->
        <button type="submit">Remember</button>
    </form>
</template>

<script setup lang="ts">
import { computed, ref, toHandlerKey, inject, onMounted } from 'vue';
import Emoticonos from '@/components/Emoticonos.vue'
import type Entry from "@/types/Entry.ts";
import type Emoji from "@/types/Emoji.ts";


//explicar
const emit = defineEmits<{
    (e: "@create", entry:Entry): void
}>();

const maxCaracters = 280
const body = ref("")
const emoji = ref <Emoji | null> (null)
const charCount = computed(() => body.value.length)
console.log(charCount)

const recollirTextForm = (e: Event)=>{
    const textarea = e.target as HTMLTextAreaElement
    if (textarea.value.length<=maxCaracters){
        body.value = textarea.value
    }
    else {

    }
}

const gestionarSubmit = ()=>{
    emit('@create', {
        body: body.value, 
        emoji: emoji.value, 
        dataCreacio: new Date(), 
        userId: 1, 
        id: Math.random()})
}
</script>