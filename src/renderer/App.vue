<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
import {getNow} from '@/api/api';

  export default {
    name: 'tuboshu-monitor',
    data(){
      return{}
    },
    created(){
        setInterval(()=>{
        this.getData()
        },1000)
    },
    methods:{
      async getData(){
        try {
          const res = await getNow({symbol:'btcusdt'})
          console.log(res);
          if(res.status === 200){
            let price = res.data.tick.data[0].price
            this.$electron.ipcRenderer.send('set-title',price)

          }
        } catch (error) {
          
        }
      } 
    }
  }
</script>

<style>
  /* CSS */
</style>
