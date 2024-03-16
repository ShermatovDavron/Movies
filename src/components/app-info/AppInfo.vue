<template>
  <Box>
    <p class="fs-3 text-uppercase">Barcha filmlar soni:{{moviesCount}}</p>
    <p class="fs-3 text-uppercase">Ko'rilgan kinolar soni:{{favouriteCount}}</p>
  </Box>
</template>

<script >
 export default {

   props:{
     moviesCount:{
       type:Number,
       required:true
     },
     favouriteCount:{
       type:Number,
       required: true
     }
   }
 }
</script>

<style scoped>

</style>