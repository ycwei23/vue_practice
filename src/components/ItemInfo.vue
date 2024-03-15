<template>
    <h1>商品資訊</h1>
    <div :style="itemInfoStyle">
        <div v-for="(spec, index) in specs" :key="index">
            {{ spec.specName }}
            <div v-for="(option, optIndex) in spec.specOptions" :key="optIndex">
                <button>{{ option.name }}</button>
            </div>
        </div> 
    </div>
</template>
  
<script>
  export default {
    props: ['specs'],
    setup(props) {
      const { specs } = props;

      const itemInfoStyle = {
        border: '1px solid #ccc',
        padding: '10px',
        marginBottom: '20px'
      };
  
      return {
        itemInfoStyle
      };
    }
  };
</script>
  