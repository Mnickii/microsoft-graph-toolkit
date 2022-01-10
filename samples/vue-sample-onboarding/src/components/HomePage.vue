<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <mgt-msal2-provider
      client-id="e25e74ba-7d3e-4a5f-bb6b-ac1ca12742f2"
      redirect-uri="http://localhost:8080"
      scopes="user.read,people.read,user.readbasic.all,contacts.read,calendars.read,files.read,group.read.all,tasks.readwrite"
    >
    </mgt-msal2-provider>

    <header>
      <h1>My Organizer</h1>
      <p>Sign-in to get started organizing your work and life.</p>
      <mgt-login v-pre>
        <template data-type="signed-out">
          <div>Sign In</div>
        </template>
      </mgt-login>
    </header>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { ProviderState, Providers } from '@microsoft/mgt';

export default defineComponent({
  name: 'HomePage',
  props: {
    msg: String,
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
