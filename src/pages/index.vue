<template>
    <h1 class="text-2xl font-bold">Welcome to Vue3Stackter, {{ name }}</h1>

    <div class="mt-8">
        <input
            v-model="newName"
            type="text"
            class="p-2 border border-gray-300 rounded focus:ring-2"
        />
        <v-button
            :class="{ 'pointer-events-none opacity-40': !newName }"
            @click.native="saveName"
        >
            Save
        </v-button>
        <button class="btn">neutral</button> 
<button class="btn btn-primary">primary</button> 
<button class="btn btn-secondary">secondary</button> 
<button class="btn btn-accent">accent</button> 
<button class="btn btn-ghost">ghost</button> 
<button class="btn btn-link">link</button>
<a href="#my-modal" class="btn btn-primary">open modal</a> 
<div id="my-modal" class="modal">
  <div class="modal-box">
    <p>Enim dolorem dolorum omnis atque necessitatibus. Consequatur aut adipisci qui iusto illo eaque. Consequatur repudiandae et. Nulla ea quasi eligendi. Saepe velit autem minima.</p> 
    <div class="modal-action">
      <a href="#" class="btn btn-primary">Accept</a> 
      <a href="#" class="btn">Close</a>
    </div>
  </div>
</div>
    </div>
</template>

<script setup>
import { useMeta } from 'vue-meta'
import { computed, ref } from 'vue'
import { useRouter } from 'vue-router'
import { useStore } from 'vuex'

useMeta({
    title: 'Homepage',
})

const router = useRouter()

const store = useStore()

// name
// const name = computed(() => store.state.user.name)
const name = computed(() => store.getters['user/nameUppercased'])
const newName = ref('')
function saveName() {
    if (newName.value === '') {
        return
    }
    store.dispatch('user/saveName', newName.value)
    newName.value = ''
    router.push(`/about/${name.value}`)
}
</script>
