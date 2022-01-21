<template>
  <div class="hello">
    <h1 v-if="signedIn">Welcome {{ name }}.</h1>
    <mgt-msal2-provider
      client-id="e25e74ba-7d3e-4a5f-bb6b-ac1ca12742f2"
      redirect-uri="http://localhost:8080"
      scopes="user.read,people.read,user.readbasic.all,
      contacts.read,calendars.read,files.read,group.read.all,tasks.readwrite"
    >
    </mgt-msal2-provider>

    <header v-if="!signedIn">
      <mgt-login v-pre>
        <template data-type="signed-out">
          <div>Sign In</div>
        </template>
      </mgt-login>
    </header>
    <div id="sidePanel" v-if="signedIn">
      <div id="profile">
        <mgt-person person-query="me" view="twoLines" line2-property="jobTitle"> </mgt-person>
        <a href="#" @click="logout()">Sign Out</a>
      </div>

      <mgt-people v-pre>
        <template>
          <ul>
            <li data-for="person in people">
              <mgt-person person-query="{{ person.userPrincipalName }}"></mgt-person>
              <h3>{{ person.displayName }}</h3>
              <p>{{ person.jobTitle }}</p>
              <p>{{ person.department }}</p>
            </li>
          </ul>
        </template>
      </mgt-people>
    </div>

    <h2 id="agendaHeader">Agenda</h2>
    <mgt-agenda class="mgt-dark" group-by-day="true"></mgt-agenda>

    <h2 id="tasksHeader">Tasks</h2>
    <mgt-tasks data-source="todo" read-only="true"></mgt-tasks>

    <h2 id="filesHeader">Files</h2>
    <mgt-file-list max-upload-file="5" enable-file-upload></mgt-file-list>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { ProviderState, Providers, MgtPerson } from '@microsoft/mgt';

export default defineComponent({
  name: 'HomePage',
  props: {
    name: String,
  },
  data() {
    return {
      signedIn: false,
      details: {},
    };
  },
  created() {
    const provider = Providers.globalProvider;
    if (provider) {
      this.loggedIn(provider.state);
      provider.onStateChanged(this.loggedIn);
    }

    Providers.onProviderUpdated(() => {
      const provider2 = Providers.globalProvider;
      if (provider2) {
        this.loggedIn(provider2.state);
        provider2.onStateChanged(this.loggedIn);
      }
    });
  },
  methods: {
    loggedIn(state: any) {
      if (state === ProviderState.SignedIn) {
        this.signedIn = true;
      }
    },
    loggedOut() {
      this.signedIn = false;
    },
    setDetails() {
      this.details = (this.$refs.user as MgtPerson).personDetails;
    },
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
