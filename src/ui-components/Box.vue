<script>
export default {
  name:"Box"
}
</script>

<template>
<div class="box">
  <slot></slot>
</div>
</template>

<style scoped>
.box {
  margin-top: 1.5rem;
  margin-bottom: 1rem;
  padding: 1.5rem;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
  background-color: #fcfaf5;
}
</style>