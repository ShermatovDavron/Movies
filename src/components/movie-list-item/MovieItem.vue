<template>
  <li class="list-group-item d-flex justify-content-between " :class="[{like:movie.like}, {favourite:movie.favourite}]">
    <span class="list-group-item-label"  @click="$emit('onToggle',{id:movie.id, prop:'like'})">{{ movie.name }}</span>
    <div class="d-flex justify-content-center align-items-content">
      <input type="number" class="list-group-item-input" :value="movie.viewers">
      <button type="button" class="btn-cookie btn-sm" @click="$emit('onToggle',{id:movie.id, prop:'favourite'})">
        <a class="fas fa-cookie btn-cookie"></a>
      </button>
      <button type="button" class="btn-trash btn-sm" @click="$emit('onRemove',movie.id)">
        <a class="fas fa-trash btn-trash"></a>
      </button>
      <i class="fas fa-star"></i>
    </div>
  </li>
</template>

<script>
import movieForm from "@/components/movie-add-form/MovieForm.vue";

export default {
  computed: {
    movieForm() {
      return movieForm
    }
  },
  props: {
    movie: {
      type: Object,
      required: true,
    }
  },

  methods:{
  }
}
</script>

<style scoped>
.list-group-item {
  padding: 15px 20px;
  border: none;
  border-bottom: 1px solid #3d5a80;
}

.list-group-item:last-child {
  border: none;
}

.list-group-item span {
  line-height: 35px;
  font-size: 20px;
  cursor: pointer;
  width: 550px;
}

.list-group-item input {
  line-height: 35px;
  font-size: 20px;
  text-align: center;
  border: 0;
  outline: hidden;
}

.list-group-item button {
  width: 35px;
  height: 35px;
  margin: 3px;
  font-size: 17px;
  border: none;
  cursor: pointer;
}

.list-group-item .btn-cookie {
  color: #e09f3e;
}

.list-group-item .btn-trash {
  color: #e5383b;
}

.list-group-item .fa-star {
  width: 35px;
  height: 35px;
  line-height: 35px;
  text-align: center;
  font-size: 16px;
  color: #ffd700;
  transition: .3s all;
  transform: translateX(30px);
  opacity: 0;
}

.list-group-item.like .fa-star {
  opacity: 1;
  transform: translateX(0);
}

.list-group-item.favourite .list-group-item-label, .list-group-item.favourite .list-group-item-input {
  color: #e09f3e;
}
</style>