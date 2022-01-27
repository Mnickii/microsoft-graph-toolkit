<template>
  <div id="profile">
    <mgt-person person-query="me" view="twoLines" line2-property="jobTitle"> </mgt-person>
    <a href="#" @click="logout">Sign Out</a>
  </div>
</template>

<script>
import { defineComponent } from 'vue';
import { Providers } from '@microsoft/mgt';

export default defineComponent({
  name: 'Profile',
  methods: {
    logout() {
      const provider = Providers.globalProvider;
      if (provider && provider.logout) {
        provider.logout();
      }
    },
  },
});
</script>

<style lang="scss"></style>
