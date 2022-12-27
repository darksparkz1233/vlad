<template>
  <div :class="{ dark: darkMode }">
    <!-- ? header -->
    <div class="">
      <NuxtLoadingIndicator />
  
    </div>

    <div class="flex flex-col gap-10 h-full bg-gray-100 dark:bg-[#030303]">
      <!-- ? first coffee row: -->
      <FirstRow class="mt-10" />
      <!-- ? second coffee row: -->
      <SecondRow class="mt-10" />
    </div>
  </div>
</template>
 
<script setup>
const darkMode = ref(true);
</script>