<template>
  <div class="container">
    <Appinfo @createObj="createFnc" />
    <h2>Bugun</h2>
    <Tasks v-for="newArr in arrData" v-bind:newArr="newArr" />
    <h2>Ertaga</h2>
    <Tasks v-for="newArr in arrData2" v-bind:newArr="newArr" />
    <h2>Keyin</h2>
    <Tasks v-for="newArr in arrData3" v-bind:newArr="newArr" />
  </div>
</template>

<script>
import Appinfo from "./app-info/Appinfo.vue";
import Tasks from "./tasks_panel/Tasks.vue";
export default {
  components: {
    Appinfo,
    Tasks,
  },
  data() {
    return {
      blogArr: ["bugun", "ertaga", "Keyin"],
      arrData: [
      ],
      arrData2: [
      ],
      arrData3: [
      ],
    };
  },
   mounted() {
    const storedArrData = localStorage.getItem("arrDataLocalStorage");
    if (storedArrData) {
      this.arrData = JSON.parse(storedArrData);
    }

    const storedArrData2 = localStorage.getItem("arrData2LocalStorage");
    if (storedArrData2) {
      this.arrData2 = JSON.parse(storedArrData2);
    }

    const storedArrData3 = localStorage.getItem("arrData3LocalStorage");
    if (storedArrData3) {
      this.arrData3 = JSON.parse(storedArrData3);
    }
  },
  methods: {
    createFnc(item) {
      const msg_obj = item.text;
      const dateRegex = /^\d{2}\/\d{2}\/\d{4}$/;
      const dataRegex2 = msg_obj.match(dateRegex) || msg_obj;
      if (msg_obj.includes("Bugun")) {
        this.arrData.push(item);
        localStorage.setItem("arrDataLocalStorage", JSON.stringify(this.arrData));
      } else if (msg_obj.includes("Ertaga")) {
        this.arrData2.push(item);
        localStorage.setItem("arrData2LocalStorage", JSON.stringify(this.arrData2));
      } else if (dataRegex2) {
        this.arrData3.push(item);
         localStorage.setItem("arrData3LocalStorage", JSON.stringify(this.arrData3));
      } else {
        arrData.push(msg_obj);
      }
    },
  },
};
</script>

<style></style>
