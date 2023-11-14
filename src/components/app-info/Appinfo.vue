<template>
<div class="data_input">
  <form class="d-flex justify-content-between" @submit.prevent>
    <input v-model="inputText" type="text" class="input_dt form-control" placeholder="Yangi vazifa qo'shish" aria-label="Example text with button addon" aria-describedby="button-addon1">
    <button @click="in_data" type="submit" class="btn">+</button>
       <!-- <div v-if="outputObj">
      <p>{{ outputObj.text }}</p>
      <p>{{ outputObj.date }}</p>
      <p>{{ outputObj.time }}</p>
    </div> -->
  </form>
  <div>
   Bugun: {{ formattedDateTime  }}
  </div>
</div>
</template>

<script>
export default{
  data(){
    return{
      hozirgiVaqt: new Date(), 
      inputText: '',
      // outputObj: null
    }
  },
  methods: {
    in_data(e) {
        const matchResult = this.inputText.match(/(\d{1,2}\/\d{1,2}\/\d{4}), (\d{1,2}:\d{2})/);
        const matchResult2 = this.inputText.match(/(\d{2}\/\d{2}\/\d{4},\s\d{2}:\d{2})/);
        let sanaVaVaqtniAjratish = /(\d{2}\/\d{2}\/\d{4},\s\d{2}:\d{2})/;
        const result = this.inputText.match(sanaVaVaqtniAjratish);
        if (result) {
         let text = this.inputText.replace(sanaVaVaqtniAjratish, "").trim();
            if (matchResult || matchResult2) {
        const [, date, time] = matchResult || matchResult2;
        
        const outputObj = {
          text: text,
          date: date,
          time: time
        };
        this.$emit('createObj', outputObj)
      } else if(!matchResult) {
          // const [,] = matchResult;
        
        const outputObj = {
          text: this.inputText,
          // date: date,
          // time: time
        };
        this.$emit('createObj', outputObj)
        // alert('Iltimos, matnni to\'g\'ri formatda kiriting: "MM/DD/YYYY, HH:mm"');
      }
        }else if (!result){
          if (matchResult) {
        const [, date, time] = matchResult;
        
        const outputObj = {
          text: this.inputText,
          date: date,
          time: time
        };
        this.$emit('createObj', outputObj)
      } else if(!matchResult) {
          // const [,] = matchResult;
        
        const outputObj = {
          text: this.inputText,
          // date: date,
          // time: time
        };
        this.$emit('createObj', outputObj)
        // alert('Iltimos, matnni to\'g\'ri formatda kiriting: "MM/DD/YYYY, HH:mm"');
      }
        }
        
    }
  },
    computed: {
    formattedDateTime: function () {
      var options = { year: 'numeric', month: '2-digit', day: '2-digit', hour: '2-digit', minute: '2-digit' };
      return this.hozirgiVaqt.toLocaleDateString('en-GB', options);
    }
  },
   mounted() {
    setInterval(() => {
      this.hozirgiVaqt = new Date();
    }, 1000);
  }
}
</script>

<style scoped>
.data_input{
  margin-top: 50px;
}
.btn{
  background-color: #89D7AD;
  border: 3px solid #04AA6D;
  font-size: 20px;
}
.input_dt{
  border: 3px solid #B3B3B3;
  margin-right: 20px;
}
</style>