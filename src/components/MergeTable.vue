<template>
  <!-- 規格合併表 -->
  <h1>規格合併表</h1>
  <div>
      <table :style="itemMergeTableStyle" border="1">
          <tr>
              <th v-for="(spec, index) in specs" :key="index">{{ spec.specName }}</th>
              <th>價格</th>
              <th>商品數量</th>
              <th>商品選項貨號</th>
              <th>GTIN</th>
          </tr>
          <tr v-for="combination in allCombinations.value">
              <td v-for="(value, key) in combination" :key="key">{{ value }}</td>
              <td><input type="text" alt="價格輸入格" placeholder="請輸入"></td>
              <td><input type="number" alt="商品數量輸入格" value="0"></td>
              <td><input type="text" alt="商品選項貨號輸入格" placeholder="請輸入"></td>
              <td><input type="text" alt="GTIN輸入格" placeholder="請輸入"></td>
          </tr>
      </table>
  </div>
  <button @click="generateCombinations">更新表格</button>
</template>

<script>

export default {
  props: ['specs', 'allCombinations'],
  setup(props) {
      const { specs, allCombinations } = props;

      const itemMergeTableStyle = {
          border: '1px solid #ccc',
          borderCollapse: 'collapse'
      };
  
      const generateCombinations = () => {
          const combinations = [];
          const specNames = specs.map(spec => spec.specName);
          generate(specNames, [], 0);
          function generate(specNames, combination, index) {
              if (index === specNames.length) {
                  const obj = {};
                  for (let i = 0; i < combination.length; i++) {
                      obj[specNames[i]] = combination[i];
                  }
                  combinations.push({ ...obj });
                  return;
              }
              const currentSpecOptions = specs[index].specOptions.map(option => option.name);
              for (const option of currentSpecOptions) {
                  generate(specNames, [...combination, option], index + 1);
              }
          }
          allCombinations.value = combinations;
      }
  
      return {
          itemMergeTableStyle,
          generateCombinations
      };
  }
};
</script>
