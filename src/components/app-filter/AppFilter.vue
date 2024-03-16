<template>
  <div class="btn-group">
    <PrimaryButton v-for="filterButton in filterButtons"
            :key="filterButton.name"
        @click="changeFilter(filterButton.name)"
        :class="[filterName===filterButton.name? 'btn-dark':'btn-outline-dark']"
        type="button">
      {{filterButton.title}}
    </PrimaryButton>
  </div>
</template>

<script>
export default {
  components:{

  },
  props: {
    updateFilterHandler: {
      type: Function,
      required: true
    },
    filterName: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      filterButtons:[
        {
          title:'Barcha kinolar',
          name:'all'
        },
        {
          title:'Mashxur kinolar',
          name:'like'
        },
        {
          title:"Eng ko'p ko'rilgan kinolar",
          name:'viewers'
        }
      ],
      filter: 'all',
    }
  },
  methods: {
    changeFilter(filter) {
      this.filter = filter
      this.updateFilterHandler(this.filter)
    }
  }
}
</script>
<style scoped>

</style>