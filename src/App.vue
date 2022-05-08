<template>
  <div class="amount-input">
    <a-input-number
      v-model="value"
      :parser="parser"
      :formatter="formatNumber"
      style="width: 100%"
    />
  </div>
</template>
<script>
export default {
  data() {
    return {
      value: ""
    };
  },
  methods: {
    parser(str) {
      if (Number(str)) {
        console.log(str);
        return str.replace(/^(\d+)(\.\d{0,2})?/g, function(str, p1, p2) {
          if (!p2) {
            return `${p1}.00`;
          } else if (p2.length === 1) {
            return `${p1}.${p2}0`;
          } else {
            return `${p1}.${p2}`;
          }
        });
      }
      return "";
    },
    formatNumber(value) {
      console.log("formatNumber:", value);
      return value.replace(/\B(?=(\d{3})+(?!\d))/g, ",");
    }
  }
};
</script>
<style lang="css">
.amount-input {
  width: 500px;
  margin: 100px auto;
}
</style>
