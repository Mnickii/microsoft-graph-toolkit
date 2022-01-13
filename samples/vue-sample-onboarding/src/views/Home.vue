<template>
  <div class="home">
    <HomePage name="Carol" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import HomePage from '@/components/HomePage.vue'; // @ is an alias to /src

export default defineComponent({
  name: 'Home',
  components: {
    HomePage,
  },
});
</script>
