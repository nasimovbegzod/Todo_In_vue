<template>
  <div class="data_input">
    <form class="d-flex justify-content-between" @submit.prevent>
      <input
        v-model="inputText"
        type="text"
        class="input_dt form-control"
        placeholder="Yangi vazifa qo'shish"
        aria-label="Example text with button addon"
        aria-describedby="button-addon1"
      />
      <button @click="in_data" type="submit" class="btn">+</button>
    </form>
    <div>Bugun: {{ formattedDateTime }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      hozirgiVaqt: new Date(),
    };
  },
  methods: {
    in_data(e) {
      const matchResult = this.inputText.match(
        /(\d{1,2}\/\d{1,2}\/\d{4}), (\d{1,2}:\d{2})/
      );
      const matchResult2 = this.inputText.match(/(\d{1,2}\/\d{1,2}\/\d{4})/);
      const matchResult3 = this.inputText.match(/(\d{1,2}:\d{2})/);
      let sanaVaVaqtniAjratish = /(\d{2}\/\d{2}\/\d{4},\s\d{2}:\d{2})/;
      let vaqtOlish = /(\d{1,2}:\d{2})/;
      let sanaOLish = /(\d{1,2}\/\d{1,2}\/\d{4})/;
      const result = this.inputText.match(sanaVaVaqtniAjratish) || this.inputText.match(vaqtOlish) || this.inputText.match(sanaOLish) ;
      if (result) {
        let text = this.inputText.replace(/[0-9\/:]/g, '').trim()
        if (matchResult || matchResult2 || matchResult3) {
          const [, date, time] = matchResult || matchResult2 || matchResult3;

          const outputObj = {
            text: text,
            date: date,
            time: time,
          };
          this.$emit("createObj", outputObj);
        } else if (!matchResult || !matchResult2 || !matchResult3) {
          const outputObj = {
            text: this.inputText,
          };
          this.$emit("createObj", outputObj);
        }
      } else if (!result) {
        if (matchResult || matchResult2 || matchResult3) {
          const [, date, time] = matchResult || matchResult2 || matchResult3;

          const outputObj = {
            text: this.inputText,
            date: date,
            time: time,
          };
          this.$emit("createObj", outputObj);
          this.inputText = "";
        } 
        else if (!matchResult || !matchResult2 || !matchResult3) {
          const outputObj = {
            text: this.inputText,
          };
          this.$emit("createObj", outputObj);
        }
      }
      this.inputText = "";
    },
  },
  computed: {
    formattedDateTime: function () {
      var options = {
        year: "numeric",
        month: "2-digit",
        day: "2-digit",
        hour: "2-digit",
        minute: "2-digit",
      };
      return this.hozirgiVaqt.toLocaleDateString("en-GB", options);
    },
  },
  mounted() {
    setInterval(() => {
      this.hozirgiVaqt = new Date();
    }, 1000);
  },
};
</script>

<style scoped>
.data_input {
  margin-top: 50px;
}
.btn {
  background-color: #89d7ad;
  border: 3px solid #04aa6d;
  font-size: 20px;
}
.input_dt {
  border: 3px solid #b3b3b3;
  margin-right: 20px;
}
</style>
