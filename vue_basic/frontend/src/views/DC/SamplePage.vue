<template>
  <div>
		<h1>Sample Page</h1>
    <button @click="apiTest">API 통신 테스트 type1</button><br/><br/>
    <button @click="apiTest2">API 통신 테스트 type2</button><br/><br/>
    <button @click="callAlert">Alert 팝업 호출</button><br/><br/>
    <button @click="callConfirm">Confirm 팝업 호출</button><br/><br/>
    <button @click="callCommonUtil">공통함수 호출</button><br/><br/>
    <button @click="openComponent">자식으로 데이터 전달</button><br/><br/>
    <child-component v-if="openActive" @close="openActive = false, testData = 0" :sendData=testData></child-component>
  
    <button @click="callAPITest">api test</button>
    <img src="http://www.e-stc.or.kr/upload/tbl_play_place/251_2.jpg">
  </div>
   
</template>

<script>

import CommonUtil from '@/common/commonUtil.js';
import childComponent from '@/views/DC/childComponent';

export default {
  name: "Example",
  components : {childComponent},
  data() {
    return {
      openActive : false,
      testData : 0,
      let: '37.51292665',
      log: '127.0648145'
    };
  },
  
  computed: {
   
  },

  watch:{

  },

  methods: {
    async apiTest(){
			let rst = await this.$MNetSend({
				url: 'pushwidgetapi/wnuri-fct2021/api/main/current-weather-array.do?code=1168058000,1162069500&unit=m/s',
			});

			console.log(rst);
    },

    async apiTest2(){
			let rst = await this.$MNetSend({
				url: `w/rest/zone/find/dong.do?x=1&y=1&lat=${this.let}&lon=${this.log}`,
			});

			console.log(rst);
    },

    async callAlert(){
      await this.$popAlert("alert 팝업");

      console.log('대기');
    },

    async callConfirm(){
      let isOK = await this.$popConfirm("confirm 팝업");

      if(isOK){
        console.log("확인 버튼을 눌렀습니다.");
      }else{
        console.log("취소 버튼을 눌렀습니다.");
      }
    },

    callCommonUtil(){
      CommonUtil.CommonFunc();
    },

    openComponent(){
      this.openActive = true;
      this.testData += 1;
    },

    async callAPITest(){
      let rst = await this.$MNetSend({
				url: `http://api.kcisa.kr/openapi/service/CNV/API_CNV_043/request?serviceKey=5b6d4464-69e0-40ae-88c1-84158f043867&numOfRows=10&pageNo=1`,
			});

			console.log(rst);
      
    }

  },

  mounted() {

  },
};
</script>

<style>

</style>
