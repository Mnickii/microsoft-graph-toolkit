<template>
  <div class="home">
    <HomePage />
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
<style scoped lang="scss">
h2, p {
  margin: 0 0 1em 0;
  font-size: 20px;
  font-weight: bold;
}
</style>
