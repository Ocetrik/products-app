<template>
  <div class="sort-product">
    <select v-model="modelValue" @change="changeOption">
      <option selected value="">По умолчанию</option>
      <option
        v-for="option in options"
        :key="option.value"
        :value="option.value"
      >
        {{ option.name }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "SortProduct",
  props: {
    modelValue: {
      type: String,
    },
    options: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    changeOption(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>

<style lang="scss" scoped>
select {
  background: #fffefb;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
  border: #ffffff;
  font-family: "SourceSansPro-Regular";
  font-size: 12px;
  line-height: 15px;
  color: #b4b4b4;
  min-width: 121px;
  min-height: 36px;
  text-align: center;

  &:hover {
    box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.3);
  }
}

option {
  color: #000000;
}
</style>