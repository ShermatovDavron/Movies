<template>
  <Box class="movie-add-form">
    <h3>Yangi kino qo'shish</h3>
    <form class="add-form d-flex" @submit.prevent>
      <Input
          class=" new-movie-label m-2"
          placeholder="Qanday kino"
          v-model="name"
      />
      <Input
          type="number"
          class="new-movie-label m-2"
          placeholder="Nechi marta ko'rilgan"
          v-model="viewers"
      />

      <PrimaryButton class="btn-outline-dark" type="submit" @click="addMovie">Qo'shish</PrimaryButton>
    </form>
  </Box>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      viewers: '',
    }
  },
  methods:{
    addMovie(){
      if (!this.name || !this.viewers) return
      const newMovie={
          name:this.name,
          viewers:this.viewers,
          favourite:false,
          like:false,
          id:Date.now()
      }
     this.$emit('createMovie',newMovie)
      this.name = ''
      this.viewers=''
    }
  },
}
</script>

<style scoped>
</style>