<template>
  <div id="app">
      <h1>在线翻译</h1>
      <h5>简单/易用/便捷</h5>
      <h6>支持中文、英语、日语、韩语、俄语、法语、葡萄牙文、西班牙文互转</h6>
      <translateForm v-on:formSubmit="tranlateText"></translateForm>
      <translateOutput v-html="translatedText"></translateOutput>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import TranslateForm from './components/translatForm'
import md5 from 'js-md5';
import translateOutput from './components/translateOutput'

export default {
  name: 'App',
  data: function(){
    return{
      date:new Date(),
      api:'https://openapi.youdao.com/api',
      appKey:'0f1875fb13394408',
      scress:'ySyUGzZQD9M35tWUrgOF0831cl9MuBwo',
      translatedText:'',
    }
  },
  components: {
    TranslateForm,
    translateOutput
  },
  methods:{
    tranlateText:function(text,formLanguafe,toLanguage){
      this.$http.jsonp(this.mixUrlParams(text,formLanguafe,toLanguage)).then((res)=>{
        console.log(res);
        if(res.ok == true && res.status == 200){
          this.translatedText = '<div class="res-box">'+
          '<div style="text-align:left;font-weight:bold;font-size:18px;">'+res.body.query+':'+res.body.translation.join('/')+'</div>'+
          (res.body.basic ? '<div class="" style="text-align:left;">'+(res.body.basic['phonetic'] ? '<span>英&nbsp;&nbsp;['+res.body.basic['phonetic']+']</span>':'')+(res.body.basic['us-phonetic'] ? '<span style="margin-left:5%;">美&nbsp;&nbsp;['+res.body.basic['us-phonetic']
+']</span>' : '')+'</div>'+(res.body.basic.explains ? this.getExlains(res.body.basic.explains):''):'')+
          '<div style="text-align:left;font-weight:bold;color:#c1c1c1;">网络释意：</div>'+
          (res.body.web ?this.formateData(res.body.web):'')+
          '</div>';
        }else{
          this.translatedText = '<div class="res-box">没有翻译结果</div>';
        }
      });
      
    },
    mixUrlParams:function(text,formLanguafe,toLanguage){
      let salt = this.date.getTime();
      let sign = md5(this.appKey+text+salt+this.scress);
      return encodeURI(this.api+'?q='+text+'&from='+formLanguafe+'&to='+toLanguage+'&appKey='+this.appKey+'&salt='+salt+'&sign='+sign);
    },
    formateData:function(data){
      let tmp = '';
      for(var i=0;i<data.length;i++){
        tmp+= '<div class="" style="text-align:left;"><span>'+data[i].key+'</span><span style="margin-left:5%;">'+data[i].value.join(', ')+'</span></div>';
      }
      return tmp;
    },
    getExlains:function(explains){
      let tmp = '';
      for(var i=0;i<explains.length;i++){
        tmp += '<div class="" style="text-align:left;">'+explains[i]+'</div>';
      }
      return tmp;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width:90%;
  margin:0 auto;
  padding:20px 0 0 0;
}
</style>
