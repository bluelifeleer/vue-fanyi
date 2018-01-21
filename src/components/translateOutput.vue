<template>
  <div class="output-text-box">
    <div id="translateOutput">
    {{translatedText}}
    </div>
  </div>
  
</template>

<script>

export default {
  name: 'translateOutput',
  props:[
  'translatedText'
  ]
}
</script>

<style>
.output-text-box{width:100%;height:300px;border:1px solid #c1c1c1;overflow: auto;margin:20px 0 0 0;}
.res-box{width:96%;height:auto;padding:2%;margin:2%;}
</style>
