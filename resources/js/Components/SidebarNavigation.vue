<script setup>
import { defineProps } from 'vue';
import { Link } from '@inertiajs/vue3';
import { inject } from 'vue';

const { hidden } = defineProps(['hidden']);
const darkTheme = inject('darkTheme')

const logout = () => {
    page.post(route('logout'), {
        _token: csrfToken.value,
    });
};
</script>

<template>
    <div :class="[darkTheme ? 'dark-main-nav' : 'light-main-nav']">
      <Link :href="route('dashboard')" :active="route().current('dashboard')" class="nav-link">
        <i class="fas fa-home"></i>
        <span :hidden="hidden" class="text-label" :class="[darkTheme ? 'dark-text' : 'light-text']"> Home</span>
      </Link>
      <Link :href="route('games.index')" :active="route().current('games.index')" class="nav-link">
        <i class="fas fa-seedling"></i>
        <span :hidden="hidden" class="text-label" :class="[darkTheme ? 'dark-text' : 'light-text']"> Plants</span>
      </Link>
      <Link :href="route('attributes.index')" :active="route().current('attributes.index')" class="nav-link">
        <i class="fas fa-hand-rock"></i>
        <span :hidden="hidden" class="text-label" :class="[darkTheme ? 'dark-text' : 'light-text']"> Plant Types</span>
      </Link>
      <Link :href="route('dateIndex')" :active="route().current('dateIndex')" class="nav-link">
        <i class="far fa-calendar-alt"></i>
        <span v-if="!hidden" class="text-label" :class="[darkTheme ? 'dark-text' : 'light-text']"> Release Dates</span>
      </Link>
      <Link :href="route('logout')" method="post" title="Logout" class="nav-link">
        <i class="fas fa-sign-out-alt"></i>
        <span :hidden="hidden" class="text-label" :class="[darkTheme ? 'dark-text' : 'light-text']"> Logout</span>
      </Link>
    </div>
</template>

<style scoped>
.light-main-nav {
  background-color: #006633; /* Darker green color for light theme */
  color: #415c5e;
}

.dark-main-nav {
  background-color: #004d40; /* Darker green color for dark theme */
  color: #46adf2;
}

.light-text {
  color: #000;
}

.dark-text {
  color: #fff;
}

.nav-link {
  transition: opacity 0.5s;
}

.nav-link-enter, .nav-link-leave-to {
  opacity: 0;
}
</style>
