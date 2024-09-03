<script setup>
import { defineProps, defineEmits } from 'vue'

defineProps(['data'])

const emit = defineEmits(['addItem'])
const addToCart = (item)=>{
  emit('addItem', item)
}
</script>
<template>
  <div class="col-md-4">
    <div class="list-group" v-for="item in data" :key="item.id">
      <a href="#" class="list-group-item list-group-item-action" @click="addToCart(item)">
        <div class="d-flex w-100 justify-content-between">
          <h5 class="mb-1">{{ item.name }}</h5>
          <small>${{ item.price }}</small>
        </div>
        <p class="mb-1">{{ item.description }}</p>
      </a>
    </div>
  </div>
</template>
