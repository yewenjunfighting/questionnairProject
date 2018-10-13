<template>
    <div>
        <h2>3.请介绍一下你自己</h2>
        <textarea name="int" cols="30" rows="10" placeholder="不少于10个字" @input="getIntr">

        </textarea>
    </div>
</template>

<script>
    export default {
        name: "introduce",
        methods: {
            getIntr: function(){
                let area = event.target;
                if(area.value){
                    this.$emit('getIntroduce', area.value);
                }
            }
        }
    }
</script>

<style scoped>

</style>