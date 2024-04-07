<template>
  <q-page class="row items-center justify-evenly">
    <example-component title="Example component" active></example-component>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

import ExampleComponent from 'components/ExampleComponent.vue';

export default defineComponent({
  name: 'IndexPage',
  props: {},
  components: {
    ExampleComponent,
  },

  setup() {
    return {};
  },
});
</script>
