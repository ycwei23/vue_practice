<template>
  <!-- 規格設定 -->
  <h1>規格</h1>
  <div :style="specCardStyle">
      <div v-for="(spec, index) in specs" :key="index">
          規格{{ index + 1 }}<input type="text" v-model="spec.specName" placeholder="規格名稱">
          <button type="button" @click="deleteSpec(index)">刪除規格</button>
          <div v-for="(option, optIndex) in spec.specOptions" :key="optIndex">
              選項{{ optIndex + 1 }}<input type="text" v-model="option.name" placeholder="選項名稱">
              <button type="button" @click="deleteOption(index, optIndex)">刪除選項</button>
          </div>
          <button type="button" @click="addOption(spec)">新增選項</button>
      </div>
      <button type="button" @click="addSpec">新增規格</button>
  </div>
</template>

<script>
import { reactive } from 'vue';

export default {
  props: ['specs'],
  setup(props, { emit }) {
      const { specs } = props;

      // 新增規格
      const addSpec = () => {
          const newSpec = reactive(new Spec(specs.length + 1, '', []));
          specs.push(newSpec);
          emit('update-specs', specs);
      };

      // 新增選項
      const addOption = (spec) => {
          spec.specOptions.push({ name: '' });
          emit('update-specs', specs);
      };

      // 刪除規格
      const deleteSpec = (index) => {
          specs.splice(index, 1);
          emit('update-specs', specs);
      };

      // 刪除選項
      const deleteOption = (index, optIndex) => {
          specs[index].specOptions.splice(optIndex, 1);
          emit('update-specs', specs);
      };

      const specCardStyle = {
          border: '1px solid #ccc',
          padding: '10px',
          marginBottom: '20px',
      };

      return {
          specs,
          addSpec,
          addOption,
          deleteSpec,
          deleteOption,
          specCardStyle
      };
  }
};

class Spec {
  constructor(specID, specName, specOptions) {
      this.specID = specID;
      this.specName = specName;
      this.specOptions = specOptions;
      this.optionsLength = specOptions.length;
  }
}
</script>
