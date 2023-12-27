<script setup>
import NewLayout from '@/Layouts/NewLayout.vue';
import Navbar from '@/Components/Navbar.vue';
import { Head, usePage } from '@inertiajs/vue3';
import { Calendar } from '@fullcalendar/core';
import dayGridPlugin from '@fullcalendar/daygrid';
import timeGridPlugin from '@fullcalendar/timegrid';

import { ref, onMounted } from 'vue';

const { events } = usePage().props;

const calendarOptions = ref({
  plugins: [dayGridPlugin, timeGridPlugin],
  initialView: 'dayGridMonth',
  events: events,
  dayRender: function (info) {
    const date = info.date.toISOString().split('T')[0];
    const event = events.find(event => event.start === date);

    if (event) {
      const cell = info.el;
      const tooltip = document.createElement('div');
      tooltip.className = 'tooltip';
      tooltip.textContent = `Release date of ${event.title}`;
      tooltip.style.display = 'block';

      cell.appendChild(tooltip);

      cell.addEventListener('mouseenter', () => {
        tooltip.style.display = 'block';
      });

      cell.addEventListener('mouseleave', () => {
        tooltip.style.display = 'none';
      });
    }
  },
});

onMounted(() => {
  const calendarEl = document.getElementById('calendar');

  if (calendarEl) {
    const calendar = new Calendar(calendarEl, calendarOptions.value);
    calendar.render();
  }
});
</script>

<style scoped>
#calendar {
  background-color: rgb(198, 230, 189); /* Soft green background */
  font-size: 15px;
  width: 65%;
  margin: 0 auto;
  margin-top: 15px;
  border-radius: 10px; /* Rounded corners */
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1); /* Soft box shadow for depth */
  padding: 20px;
}

.tooltip {
  position: absolute;
  top: -20px;
  left: 20px;
  background-color: white;
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 5px;
  box-shadow: 0 0 5px rgb(46, 129, 147);
}

.fade-in {
  animation: fadeIn 0.5s ease-in-out;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

.banner {
  background-color: #4CAF50; /* Green background color for the banner */
  color: white;
  padding: 10px;
  text-align: center;
  border-radius: 10px;
  margin-bottom: 20px;
}
</style>

<template>
  <Head title="Dashboard" />

  <NewLayout>
    <Navbar />
    <div class="fade-in">
      <div class="max-w-7xl">
        <div class="bg-gray-100">
          <div class="banner">
            <h2 class="text-xl font-semibold">Explore Available Plants in Your Garden</h2>
            <p>Plan your gardening activities with the calendar below.</p>
          </div>
          <div class="p-10 text-white" id="calendar"></div>
        </div>
      </div>
    </div>
  </NewLayout>
</template>
