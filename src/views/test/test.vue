<template>
    <div class="contain">
        <h2>Vue的input框实现防抖</h2>
        <input type="text" v-model="text" />
        <p class="result">{{ text }}</p>
    </div>
</template>
<script setup>
    import { customRef } from 'vue';
    //实现防抖函数
    const debounceRef=(value,delay=1000)=>{
        let timer;
        /*
        自定义customRef实现响应式并且防抖
         @param track收集依赖
         @param trigger触发更新
        */
        return customRef((track,trigger)=>{
            return {
                get(){
                    track()
                    return value
                },
                set(val){
                    clearTimeout(timer);
                    timer=setTimeout(()=>{
                        value=val
                        trigger()
                    },delay)
                }
            };
        });
    };
    const text=debounceRef('');
</script>
<style scoped>
</style>