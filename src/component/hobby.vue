<template>
    <div @click="getHobby">
        <h2>2.你的爱好是：</h2>
        <p><label>看书<input type="checkbox" value="看书"></label></p>
        <p><label>打篮球<input type="checkbox" value="打篮球"></label></p>
        <p><label>听音乐<input type="checkbox" value="听音乐"></label></p>
        <p><label>看电影<input type="checkbox" value="看电影"></label></p>
        <p><label>跑步<input type="checkbox" value="跑步"></label></p>
        <p><label>打游戏<input type="checkbox" value="打游戏"></label></p>
    </div>

</template>

<script>
    export default {
        name: "hobby",
        methods: {
            getHobby: function(){
                let tar = event.target;
                if(tar.getAttribute('value')){
                    this.$emit('getHobby', tar.getAttribute('value'));
                }
            }
        }
    }
</script>

<style scoped>

</style>