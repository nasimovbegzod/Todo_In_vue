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
      <p :class="{ line_top: isHighlighted }">{{ newArr.time }}</p>
      <p :class="{ line_top: isHighlighted }">{{ newArr.date }}</p>
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
  methods: {
    line_top_fnc() {
      this.isHighlighted = !this.isHighlighted;
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
