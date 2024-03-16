<script >
export default {
  name:"Input",
  methods:{
    updateInput(e){
      this.$emit('update:modelValue', e.target.value)
    }
  },
  props:{
    modelValue:[String,Number]
  }
}
</script>

<template>
<input type="text" class="form-control" :value="modelValue" @input="updateInput">
</template>

<style scoped>

</style>