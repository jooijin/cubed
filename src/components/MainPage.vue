<template>
  <div class="main">
    <div id="dateArea">
      <p>조회기간을 입력해주세요!</p>
      <div>
        <input v-model="startDate">
        <input v-model="endDate">
      </div>
    </div>
    <div id="keyArea">
      <p>API Key를 입력해주세요!</p>
      <input v-model="apiKey">
    </div>
    <button @click="countCubes">GO!</button>

    <div>
      <p>당신이 사용한 블랙 큐브: </p> 
      <p>당신이 사용한 레드 큐브: </p>
      <p>당신이 사용한 에디셔널 큐브: {{ additionalCube }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainPage',
  data() {
    return{
      startDate: '',
      endDate: '',
      apiKey: '',
      additionalCube: 0,

    }
  },
  methods: {
    countCubes() {
      //Todo 날짜계산으로 바꾸기
      for(let i = this.startDate; i<this.endDate; i++) {
        this.getUsedCubes(i);
      }
    },
    getUsedCubes(date) {
      let url = 'https://public.api.nexon.com/openapi/maplestory/v1/cube-use-results';

      const params = {
        count: 1000,
        date: date
      };

      this.$axios({
        method: 'get', //you can set what request you want to be
        url: url,
        data: {params},
        headers: {
          Authorization: this.apiKey
        }
      }).then((res) => {
        if(res.status == 200){
          this.additionalCube += 1;
        } else {
          // Todo 얼럿창
        }
      }).catch();
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
#dateArea {
  ;
}

</style>
