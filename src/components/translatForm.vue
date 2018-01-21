<template>
  <div id="translateForm">
    <form v-on:submit="formSubmit($event)">
      <select name="language-select" v-model="formLanguage" class="form-control" id="exampleSelect1">
        <option value="zh-CHS">中文</option>
        <option value="ko">韩语</option>
        <option value="ja">日语</option>
        <option value="ru">俄语</option>
        <option value="EN">英文</option>
        <option value="fr">法文</option>
        <option value="pt">葡萄牙文</option>
        <option value="es">西班牙文</option>
      </select>
      <input type="text" class="form-control form-control-lg" name="" v-model="textToTranlate" value="" placeholder="请输入要翻译的内容">
      <select name="language-select" v-model="toLanguage" class="form-control" id="exampleSelect1">
        <option value="zh-CHS">中文</option>
        <option value="ko">韩语</option>
        <option value="ja">日语</option>
        <option value="ru">俄语</option>
        <option value="EN">英文</option>
        <option value="fr">法文</option>
        <option value="pt">葡萄牙文</option>
        <option value="es">西班牙文</option>
      </select>
      <input type="submit" class="submit-but btn btn-primary btn-lg" name="" value="翻译" />
    </form>
  </div>
</template>

<script>

export default {
  name: 'TranslateForm',
  data: function(){
    return {
      textToTranlate:'',
      formLanguage:'EN',
      toLanguage:'zh-CHS'
    }
  },
  methods: {
    formSubmit:function(e){
      e.preventDefault();
      this.$emit("formSubmit",this.textToTranlate,this.formLanguage,this.toLanguage);
      // alert(this.textToTranlate);
    }
  }
}
</script>

<style>
  .submit-but{width:100%;margin:20px 0 0 0;}
</style>
