<template>
  <div class="wrapper">
    <div class="people-header">
      <h2>
        Hello,
        <mgt-person person-query="me" v-pre>
          <template>
            <div>{{ person.displayName }}! 🤗</div>
          </template>
        </mgt-person>
      </h2>
      <h2>Meet the team</h2>
      <mgt-people v-pre>
        <template>
          <ul class="people-list">
            <li data-for="person in people">
              <mgt-person person-query="{{ person.userPrincipalName }}"
              person-card="hover" show-presence></mgt-person>
            </li>
          </ul>
        </template>
      </mgt-people>
    </div>

    <div class="agenda-header">
      <h2>Your Upcoming Events</h2>
      <mgt-agenda class="mgt-dark" group-by-day="true"></mgt-agenda>
    </div>
    <div class="files-header">
      <h2>Your Shared Files</h2>
      <mgt-file-list max-upload-file="5" enable-file-upload></mgt-file-list>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'HomePage',
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
*, *:before, *:after {
  box-sizing: border-box;
}

body {
  margin: 40px;
  font-family: "Circular-Bold", sans-serif;
  background-color: #fff;
  color: #444;
}

h2, p {
  margin: 0 0 1em 0;
  font-size: 20px;
  font-weight: bold;
}
li mgt-person {
    --avatar-size: 80px;
  }

.wrapper {
  max-width: 940px;
  margin: 0 20px;
  display: grid;
  grid-gap: 10px;
}
ul.people-list {
  list-style: none;
}
ul.people-list li {
  display: inline-block;
  padding: 0 0.5rem;
}
mgt-agenda {
--agenda-header-color: black;
--agenda-header-font-size: 20px;

}
@media screen and (min-width: 500px) {

  /* no grid support? */
  .files-header {
    float: left;
    width: auto;
  }

  .agenda-header {
    float: right;
    width: auto;
  }

  .wrapper {
    margin: 0 auto;
    grid-template-columns: 3fr 1fr;
  }

  .people-header {
    grid-column: 1 / -1;
    /* needed for the floated layout */
    clear: both;
  }

}

.wrapper > * {
  background-color: #fff;
  color: #000;
  border-radius: 5px;
  border-color: #444;
  padding: 20px;
  /* needed for the floated layout*/
  margin-bottom: 10px;
}

/* We need to set the widths used on floated items back to auto,
 and remove the bottom margin as when we have grid we have gaps. */
// @supports (display: grid) {
//   .wrapper > * {
//     width: auto;
//     margin: 0;
//   }
// }
</style>
