<template>
  <div>
    <mgt-msal2-provider
      client-id="e25e74ba-7d3e-4a5f-bb6b-ac1ca12742f2"
      redirect-uri="http://localhost:8080"
      scopes="user.read,people.read,user.readbasic.all,contacts.read,
      calendars.read,files.read,group.read.all,tasks.readwrite"
    >
    </mgt-msal2-provider>
    <header class="start" v-if="!signedIn">
      <h2>Onboarder App</h2>
      <p>Sign-in to get started.</p>
      <mgt-login></mgt-login>
    </header>
    <tabs v-if="signedIn"
      @onHome="setTab('Home')" @onReader="setTab('Reader')" />
    <div v-if="signedIn" class="row">
      <div class="col-sm-8">
      </div>
      <div class="col-sm-4">
        <button type="button" class="btn btn-light" @click="logout()">Sign Out</button>
      </div>
    </div>
    <home v-if="activeTab === 'Home' && signedIn" />
    <reader v-if="activeTab === 'Reader' && signedIn" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { ProviderState, Providers } from '@microsoft/mgt';
import Tabs from './components/Tabs.vue';
import Home from './views/Home.vue';
import Reader from './views/Reader.vue';

export default defineComponent({
  name: 'App',
  components: {
    Tabs,
    Home,
    Reader,
  },
  data() {
    return {
      activeTab: 'Home',
      signedIn: false,
      showProfile: false,
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
    setTab(tab: string) {
      this.activeTab = tab;
    },
    loggedIn(state: any) {
      if (state === ProviderState.SignedIn) {
        this.signedIn = true;
      } else if (state === ProviderState.SignedOut) {
        this.signedIn = false;
      }
    },
    logout() {
      const provider = Providers.globalProvider;
      if (provider && provider.logout) {
        provider.logout();
      }
    },
  },
});
</script>

<style lang="scss">
#app {
  font-family: "Circular-Bold", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.start {
  margin-top: 48px;
}

.btn {
  font-family: "Circular-Bold", sans-serif;
  margin-right: 50%;
}
.text-left {
  text-align: left;
}
.tabs {
  display: flex;
}

h2, h3, p {
  font-family: "Circular-Bold", sans-serif;
  font-size: 20px;
  font-weight: bold;
}
</style>
