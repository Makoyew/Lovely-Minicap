<script setup>
import { ref, provide } from 'vue';
import SidebarNavigation from '@/Components/SidebarNavigation.vue';
import { watch } from 'vue';

let width = ref('w-[250px]')
let hide = ref(false)

function toggleWidth() {
    if(width.value == 'w-[250px]') {
        width.value = 'w-[90px]'
        hide.value = true
    }else {
        width.value = ['w-[250px]']
        hide.value = false
    }
}

const storedTheme = localStorage.getItem('darkTheme')
const darkTheme = ref(storedTheme !== null ? JSON.parse(storedTheme) : false)
watch(darkTheme, (newValue) => {
    localStorage.setItem('darkTheme', newValue)
})
provide('darkTheme', darkTheme)

</script>

<template>
    <div>
        <div class="flex min-h-screen">
            <div id="sidebar" :class="[darkTheme ? 'dark-sidebar' : 'light-sidebar', width]" style="position: relative;">
                <button class="text-xl text-gray-600" @click="toggleWidth" style="position: absolute; right: 10px; top:10px">
                    <i :class="[darkTheme ? 'fa-solid fa-bars text-gray-500' : 'fa-solid fa-bars text-gray-600']"></i>
                </button>
                <div id="branding" :hidden="hide" class="my-6">
                    <img src="https://previews.123rf.com/images/urfandadashov/urfandadashov1808/urfandadashov180819112/108271443-plant-vector-icon-isolated-on-transparent-background-plant-logo-concept.jpg" alt="Logo"
                        class="w-[170px] h-[170px] mx-auto rounded-full object-cover">
                </div>
                <hr class="border-gray-600" :hidden="hide">
                <SidebarNavigation :hidden="hide" />
            </div>

            <div id="container" :class="[darkTheme ? 'flex-1 bg-gray-700' : 'flex-1 bg-gray-200']">
                <slot />
            </div>
        </div>
    </div>
</template>
<style scoped>
.light-sidebar {
    background-color: #006633; /* Darker green color for light theme */
  color: #415c5e;
}

.dark-sidebar {
    background-color: #004d40; /* Darker green color for dark theme */
  color: #46adf2;
}
</style>
