<template>
  <div class="hello">
    <h3>{{ msg }}</h3>
    <hr />
    <div>toRefs</div>
    <div>{{ count }}</div>
    <div>{{ double }}</div>
    <button @click="increase">click</button>
    <hr />
    <ul>
      <li v-for="(number, index) in numbers" :key="index">{{ number }}</li>
    </ul>
    <h4>{{ person.name }}</h4>
  </div>
</template>

<script lang="ts">
import { defineComponent, watch, computed, reactive, toRefs, onMounted, onUpdated, onRenderTriggered, onRenderTracked, onBeforeMount } from 'vue';
interface DataProps {
  count: number;
  double: number;
  increase: () => void;
  numbers: number[];
  person: { name?: string };
}
export default defineComponent({
  name: 'ToRefs',
  props: {
    msg: String
  },
  setup() {
    // reactive
    const data: DataProps = reactive({
      count: 0,
      double: computed(() => data.count * 2),
      increase: () => {
        data.count++;
        data.numbers[data.count] = data.count;
        data.person.name = 'loewe0202 -- ' + data.count;
      },
      numbers: [0, 1, 2],
      person: {}
    });

    // toRefs
    const refData = toRefs(data);

    watch([() => data.count, data.person], ([newVal, newVal1], [oldVal, oldVal1]) => {
      console.log('watch: -- ', newVal, oldVal, newVal1, oldVal1);
    });

    watch(data.numbers, (newVal, oldVal) => {
      console.log('watch: --- ', newVal, oldVal);
    });

    onBeforeMount(() => {
      console.log('onBeforeMount');
    });

    onMounted(() => {
      console.log('mounted');
    });

    onUpdated(() => {
      console.log('updated');
    });

    onRenderTracked(event => {
      console.log('onRenderTracked: ', event);
    });

    onRenderTriggered(event => {
      console.log('onRenderTriggered: ', event);
    });

    return {
      ...refData
    };
  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.hello {
  color: salmon;
  background: rgba(255, 0, 0, 0.3);
  padding: 15px 0;
}
</style>
