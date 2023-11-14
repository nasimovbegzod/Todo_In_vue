<template>
  <div>
    <div class="cards d-flex justify-content-between align-items-center">
      <input
        class="form-check-input fs-4"
        v-model="isHighlighted"
        @click="line_top_fnc"
        type="checkbox"
      />
      <h5 :class="{ line_top: isHighlighted }">{{ newArr.text }}</h5>
      <p :class="{ line_top: isHighlighted }">{{ newArr.date }}</p>
      <p :class="{ line_top: isHighlighted }">{{ newArr.time }}</p>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    newArr: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      isHighlighted: false,
    };
  },
   mounted() {
    const StorageKey = `highlighted_${this.newArr.id}`;
    const gedState = localStorage.getItem(StorageKey);
    if (gedState) {
      this.isHighlighted = JSON.parse(gedState);
    }
  },
  methods: {
    line_top_fnc() {
      this.isHighlighted = !this.isHighlighted;
        const StorageKey = `highlighted_${this.newArr.id}`;
      localStorage.setItem(StorageKey, JSON.stringify(this.isHighlighted));
    },
  },
};
</script>
<style scoped>
.line_top {
  text-decoration: line-through;
  color: rgb(154, 153, 153);
}
.cards{
 padding: 20px 20px;
}
</style>
