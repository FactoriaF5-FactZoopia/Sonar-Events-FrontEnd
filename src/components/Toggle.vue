<script setup></script>

<template>
  <div>
    <label class="inline-flex items-center cursor-pointer">
      <input
        type="checkbox"
        v-model="showPastEvents"
        @change="toggleEvents"
        class="sr-only peer"
      />
      <div
        class="relative w-14 h-7 bg-[#301f35] peer-focus:outline-none peer-focus:ring-4 peer-focus:ring-[white] dark:peer-focus:ring-[white] rounded-full peer dark:bg-[#301f35] border border-[white] peer-checked:bg-[#d43089] peer-checked:after:translate-x-full rtl:peer-checked:after:-translate-x-full peer-checked:after:border-[white] after:content-[''] after:absolute after:top-0.5 after:start-[4px] after:bg-[white] after:border-[white] after:border after:rounded-full after:h-6 after:w-6 after:transition-all dark:border-[white]"
      ></div>
    </label>

    <div v-if="showPastEvents">
      <h1>Past Events</h1>
      <ul>
        <li v-for="event in pastEvents" :key="event.id">{{ event.name }}</li>
      </ul>
    </div>
  </div>
</template>

<style scoped></style>
