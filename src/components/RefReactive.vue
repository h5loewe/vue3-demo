<template>
  <div class="hello">
    <h3>RefReactive demo</h3>
    <hr />
    <div>ref</div>
    <div>{{ count }}</div>
    <div>{{ double }}</div>
    <button @click="increase">click</button>
    <hr />
    <div>reactive</div>
    <div>{{ data.count }}</div>
    <div>{{ data.double }}</div>
    <button @click="data.increase">click</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed, reactive } from 'vue';
interface DataProps {
  count: number;
  double: number;
  increase: () => void;
}
export default defineComponent({
  name: 'RefReactive',
  props: {
    msg: String
  },
  setup() {
    // ref
    const count = ref(0);
    const double = computed(() => count.value * 2);
    const increase = () => count.value++;

    // reactive
    const data: DataProps = reactive({
      count: 0,
      double: computed(() => data.count * 2),
      increase: () => {
        data.count++;
      }
    });
    return {
      count,
      double,
      increase,
      data
    };
  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.hello {
  padding: 15px 0;
  color: salmon;
  background: rgba(0, 255, 1, 0.3);
}
</style>
