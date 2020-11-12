<template>
  <div class="home">
    <RefReactive />
    <ToRefs msg="props of msg" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import RefReactive from '@/components/RefReactive.vue';
import ToRefs from '@/components/ToRefs.vue';
export default defineComponent({
  name: 'Home',
  components: {
    ToRefs,
    RefReactive
  }
});
</script>
