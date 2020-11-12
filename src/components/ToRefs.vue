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
import { defineComponent, computed, reactive, toRefs, onMounted, onUpdated, onRenderTriggered } from 'vue';
interface DataProps {
  count: number;
  double: number;
  increase: () => void;
  numbers: number[];
  person: { name?: string };
  [propName: string]: any;
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
      },
      numbers: [0, 1, 2],
      person: {}
    });
    data.numbers[3] = 12;
    data.person.name = 'loewe0202';
    setTimeout(() => {
      data.numbers[4] = 26;
      data.person.name = '-- loewe0202 --';
    }, 2500);

    onMounted(() => {
      console.log('mounted');
    });

    onUpdated(() => {
      console.log('updated');
    });

    onRenderTriggered(event => {
      console.log(event);
    });

    // toRefs
    const refData = toRefs(data);
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
