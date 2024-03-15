<template>
  <div id="app">
    <div style="width: auto;">
      <SpecSetting :specs="specs" />
    </div>
    <div style="width: auto;">
      <ItemInfo :specs="specs" />
    </div>
    <div style="width: auto;">
      <MergeTable :specs="specs" :allCombinations="allCombinations" />
    </div>
    
  </div>
</template>

<script>
import { ref } from 'vue';
import SpecSetting from './components/SpecSetting.vue';
import ItemInfo from './components/ItemInfo.vue';
import MergeTable from './components/MergeTable.vue';

export default {
  components: {
    SpecSetting,
    ItemInfo,
    MergeTable
  },
  setup() {
    const specs = ref([]);

    const allCombinations = ref([]);

    return {
      specs,
      allCombinations
    };
  }
};
</script>

