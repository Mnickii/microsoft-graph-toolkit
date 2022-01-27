<template>
  <div class="reader">
    <h2 class="reader-header">Your Reading List</h2>
    <mgt-tasks data-source="todo" v-pre></mgt-tasks>
    <!-- <mgt-tasks data-source="todo" v-pre>
      <template data-type="task-details">
        <div>
          <a
            target="_"
            :href="task.subject">{{task.subject}}</a>
        </div>
      </template>
    </mgt-tasks> -->
  </div>
</template>
<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'Reader',
});
</script>
<style scoped lang="scss">
.reader-header {
  display: flex;
  justify-content: center;
  margin-right: 60px;
}
</style>
