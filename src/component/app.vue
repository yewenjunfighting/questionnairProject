<template>
<div v-show="true">
    <div v-show="now === 'gender'">
        <!--用getGender这个自定义事件来向父组件传值-->
       <gender @getGender="setGender"/>
      <div class="bt">
          <button :disabled="gd === ''" @click="down" >下一页</button>
          <button :disabled="gd === ''" @click="st">重置</button>
      </div>
    </div>
    <div v-show="now === 'hobby'">
        <hobby @getHobby="setHobby"/>
        <div class="bt">
            <button @click="up">上一页</button>
            <button :disabled="hb.length === 0" @click="down">下一页</button>
            <button @click="st" :disabled="hb.length === 0">重置</button>
        </div>
    </div>
    <div v-show="now === 'introduce'">
       <introduce @getIntroduce="setIntroduce"/>
       <div class="bt">
           <button @click="up">上一页</button>
           <button :disabled="it.length < 10" @click="st">重置</button>
           <button :disabled="it.length < 10" @click="submit">提交</button>
       </div>
    </div>
</div>
</template>
<script>
    import gender from "./gender.vue" //引入组件
    import hobby from "./hobby.vue"
    import introduce from "./introduce.vue"
    export default {
        name: 'app',
        data: function(){
            return {
                now : 'gender',
                arr: ['gender', 'hobby', 'introduce'],
                gd: '',
                hb: [],
                it: '',
                next: true,
                set: true
            }
        },
        components: {
          gender, introduce, hobby
        },
        methods: {
            up: function(){
                if(this.now === 'hobby'){
                    this.now = 'gender';
                }else this.now = 'hobby';
            },
            down: function(){
                if(this.now === 'gender'){
                    this.now = 'hobby';
                }else this.now = 'introduce';
            },
            st: function(){
                //给子组件传参数
                if(this.now === 'gender'){
                    let bt = document.querySelectorAll("input");
                    let len = bt.length;
                    console.log(len);
                    for(let i = 0;i < len; i ++){
                        if(bt[i].getAttribute('value') === this.gd){
                            bt[i].checked = false;
                            this.gd = '';
                            break;
                        }
                    }
                }else if(this.now === 'hobby'){
                    let bt = document.querySelectorAll("input");
                    let len = bt.length;
                    console.log(len);
                    for(let i = 3;i < len; i ++){
                        bt[i].checked = false;
                    }
                    this.hb = [];
                }else {
                    let textarea = document.querySelector("textarea");
                    textarea.value = '';
                    this.it = '';
                }
            },
            setGender: function(value){
                this.gd = value;
                console.log(value);
            },
            setHobby: function(value){
                //这里要注意取消选择的情况
                if(this.hb.indexOf(value) === -1){
                    this.hb.push(value);
                }else {
                    //取消选择了就把数组里的该项删掉
                    //用filter过滤一遍
                    this.hb = this.hb.filter(function(item){
                        if(item === value) return false;
                        else return true;
                    });
                }
                console.log(this.hb, this.hb.length);
            },
            setIntroduce: function(value){
                this.it = value;
                console.log(this.it);
            },
            submit: function(){
                let inf = {
                    gender: this.gd,
                    hobby: this.hb,
                    introduce: this.it
                };
                fetch('result.html')
                .then(function(response){
                        if(!response.ok) return new Error(response);
                        else window.location.href = response.url; //实现页面的跳转
                    })
            }
        }
    }
</script>
<style lang="scss" >
    button{
        padding: 2px 5px;
        border-radius: 2px;
        border:none;
        margin-right:10px;
        background-color: #fff;
    }

    button {
      cursor: pointer;
    }

    [disabled]{
        cursor: default;
    }
    .bt{
        margin-top: 20px;
    }
</style>