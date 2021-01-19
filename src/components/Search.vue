<template>
  <div class="search">
    <a @click="checkAvailability(element.manufacturer, element.id.toUpperCase())"
       v-if="!searching && !complete && !failed">
      SEARCH
    </a>
    <div v-if="searching" class="bar"></div>
    <p v-if="complete && !failed">
      {{ this.result }}
    </p>
    <p v-if="failed && !searching">
      SOMETHING WENT WRONG...
    </p>
    <a @click="checkAvailability(element.manufacturer, element.id.toUpperCase())"
       v-if="failed && !searching">
      TRY AGAIN
    </a>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Search",
  props: {
    element: Object
  },
  data() {
    return {
      result: String,
      searching: false,
      complete: false,
      failed: false
    }
  },
  methods: {
    async checkAvailability(manufacturer, id) {
      console.log('checking availability')
      this.searching = true;
      let url = `https://api.allorigins.win/get?url=https://bad-api-assignment.reaktor.com/v2/availability/${manufacturer}`;
      await axios.get(url)
          .then(data => {
            data = JSON.parse(data.data.contents);
            this.searching = false;
            try{
              let index = data.response.findIndex(element => element.id === id)
              this.result = this.formatDatapayload(data.response[index].DATAPAYLOAD);
              this.complete = true;
            }catch (err){
              console.log(err)
              this.failed = true;
            }
          })
          .then(function () {console.log('done')})
          .catch(err => {
            this.failed = true;
            console.error(err)
          })
    },
    formatDatapayload(data){
      let format = data.split("");
      format.splice(0, 50)
      for (let i = 0; i <= 30; i++) format.pop();
      return format.join('');
    },
  }
}
</script>

<style scoped>
a{
  text-decoration: underline;
  cursor: pointer;
}
.bar{
  background-color: white;
  width: 40px;
  height: 4px;

  animation: loading 1s ease-in-out infinite;
}
@keyframes loading {
  0%{
    transform: translatex(0);
    width: 20px;
  }
  25%{
    width: 40px;
  }
  50%{
    transform: translatex(-80px);
    width: 20px;
  }
  75%{
    width: 40px;
  }
  100%{
    transform: translatex(0);
    width: 20px;
  }
}
</style>