<template>
  <div id="app">
    <div class="container">
      <h1>在线翻译</h1>
      <h5>简单/易用/便捷</h5>
    </div>
    <translate-form v-on:formHandle="translateText"></translate-form>
    <translateOutput v-text="translatedText"></translateOutput>
  </div>
</template>

<script>

import TranslateForm from './components/TranslateForm'
import TranslateOutput from './components/TranslateOutput'

export default {
  name: 'App',
  data(){
    return{
      translatedText:""
    }
  },
  components: {
    "translate-form":TranslateForm,
    "translateOutput":TranslateOutput
  },
  methods:{
    translateText:function(text,language){
      //alert(text);
      this.$http.get('https://translate.yandex.net/api/v1.5/tr.json/translate?key=trnsl.1.1.20180430T090121Z.c43a651184a752dd.30c98904bbfc889b99e1331259883ff167a0c6ba&lang='+language+'&text='+text)
      .then((response)=>{
        //console.log(response.body.text[0]);
        this.translatedText = response.body.text[0];
      })
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
}
</style>
