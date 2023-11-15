<template>
  <div class="container">
    <Appinfo @createObj="createFnc" />
    <h2>Bugun</h2>
    <Tasks v-for="newArr in arrData" v-bind:newArr="newArr" />
    <h2>Ertaga</h2>
    <Tasks v-for="newArr in arrData2" v-bind:newArr="newArr" />
    <h2>Keyin</h2>
    <Tasks v-for="newArr in arrData3" v-bind:newArr="newArr" />
    <div>
      <p>Vazifalar: {{ arrData.length + arrData2.length + arrData3.length}}</p>
    </div>
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
      arrData: [],
      arrData2: [],
      arrData3: [],
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

     this.loadLocalStorageData();
    window.addEventListener("storage", this.handleLocalStorageChange);
  },
  methods: {
    createFnc(item) {
      const msg_obj = item.text;
      const msg_obj2 = item.date

      // const dateRegex = /^\d{2}\/\d{2}\/\d{4}$/;
      // const dataRegex2 = msg_obj2.match(dateRegex !== undefined);
      // const dataRegex3 = msg_obj.match(dateRegex)


      if (msg_obj === "") {
        return;
      }

      if (item.time === undefined) {
        const currentTime = new Date();
        const currentHour = currentTime.getHours();
        const currentMinutes = currentTime.getMinutes();
        let roundedHour = currentHour;

        if (currentMinutes >= 0) {
          roundedHour += 1;
        }

        roundedHour = roundedHour === 24 ? 0 : roundedHour;

        item.time = `${roundedHour}:00`;
      } else if (item.time) {
        item.time = item.time;
      }

      if (msg_obj.includes("Bugun") || msg_obj.includes("bugun")) {
        this.arrData.push(item);
        localStorage.setItem(
          "arrDataLocalStorage",
          JSON.stringify(this.arrData)
        );
      } else if (msg_obj.includes("Ertaga") || msg_obj.includes("ertaga")) {
        this.arrData2.push(item);
        localStorage.setItem(
          "arrData2LocalStorage",
          JSON.stringify(this.arrData2)
        );
      } else if (msg_obj2 && msg_obj2.match(/^\d{2}\/\d{2}\/\d{4}$/)) {
        this.arrData3.push(item);
        localStorage.setItem(
          "arrData3LocalStorage",
          JSON.stringify(this.arrData3)
        );
      } else {
        this.arrData.push(item);
        localStorage.setItem(
          "arrDataLocalStorage",
          JSON.stringify(this.arrData)
        );
      }
    },
    ///////////////////

    loadLocalStorageData() {
      this.loadLocalStorage("arrDataLocalStorage", this.arrData);
      this.loadLocalStorage("arrData2LocalStorage", this.arrData2);
      this.loadLocalStorage("arrData3LocalStorage", this.arrData3);
    },
    loadLocalStorage(key, arr) {
      const storedArrData = localStorage.getItem(key);
      if (storedArrData) {
        arr = JSON.parse(storedArrData);
      }
    },
    handleLocalStorageChange(event) {
      if (event.key === "arrDataLocalStorage") {
        this.loadLocalStorage("arrDataLocalStorage", this.arrData);
      } else if (event.key === "arrData2LocalStorage") {
        this.loadLocalStorage("arrData2LocalStorage", this.arrData2);
      } else if (event.key === "arrData3LocalStorage") {
        this.loadLocalStorage("arrData3LocalStorage", this.arrData3);
      }}
  },
};
</script>

<style></style>
