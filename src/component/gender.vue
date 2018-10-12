<template>
  <div @click="getValue">
      <h2>1.请问你的性别是：</h2>
      <label>男<input type="radio" name="gender" value="男"></label>
      <label>女<input type="radio" name="gender" value="女"></label>
      <label>保密<input type="radio" name="gender" value="secret"></label>
  </div>
</template>

<script>
    export default {
        name: "gender",
        methods: {
            getValue: function(){
                let tar = event.target;
                if(tar.name){ //点击label的区域，click会触发两次，这里是为了把label激发的click过滤掉
                    this.$emit('getGender', tar.getAttribute('value')); //通过自定义事件向外激发一个事件
                }
            }
        }
    }
</script>

<style scoped>

</style>