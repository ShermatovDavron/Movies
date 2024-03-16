<template>
<input type="text" placeholder="Kinolarni qidirish" class="form-control search-input" :value="term"  @input="changeHandler">
</template>

<script>
    export default {
      props:{
        updateTermHandler:{
          type:Function,
          required:true
        }
      },
      data(){
        return {
          term:'',
        }
      },
      methods:{
        changeHandler(e){
          this.term = e.target.value
          this.updateTermHandler(this.term)
        }
      }
    }
</script>

<style scoped>
.search-input{
  margin-top: 1rem;
  margin-bottom: 1rem;
  padding: 1.5rem;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
  background-color: #fcfaf5;
}
</style>