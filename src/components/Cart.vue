<script setup>
import { computed, ref, defineProps, defineEmits } from 'vue'

const props = defineProps(['cart'])

const noteText = ref('')

const totalPrice = computed(() => {
  let sum = 0
  for (let i = 0; i < props['cart'].length; i++) {
    sum += props['cart'][i].price * props['cart'][i].count
  }
  return sum
})

const emit = defineEmits(['deleteItem', 'createOrder'])
const deleteFromCart = (item) => {
  emit('deleteItem', item)
}
const createNewOrder = (total, note) => {
  emit('createOrder', total, note)
  noteText.value = ''
}
</script>
<template>
  <div class="col-md-8">
    <table class="table">
      <thead>
        <tr>
          <th scope="col" width="50">操作</th>
          <th scope="col">品項</th>
          <th scope="col">描述</th>
          <th scope="col" width="90">數量</th>
          <th scope="col">單價</th>
          <th scope="col">小計</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in cart" :key="index">
          <td>
            <button type="button" class="btn btn-sm" @click="deleteFromCart(index)">x</button>
          </td>
          <td>{{ item.name }}</td>
          <td>
            <small>{{ item.description }}</small>
          </td>
          <td>
            <select class="form-select" v-model="item.count">
              <option v-for="n in 10" :value="n" :key="n">{{ n }}</option>
            </select>
          </td>
          <td>{{ item.price }}</td>
          <td>{{ item.price * item.count }}</td>
        </tr>
      </tbody>
    </table>
    <div v-if="cart.length">
      <div class="text-end mb-3">
        <h5>
          總計: <span>${{ totalPrice }}</span>
        </h5>
      </div>
      <textarea class="form-control mb-3" rows="3" placeholder="備註" v-model="noteText"></textarea>
      <div class="text-end">
        <button class="btn btn-primary" @click="createNewOrder(totalPrice, noteText)">送出</button>
      </div>
    </div>
    <div v-else class="alert alert-success text-center" role="alert">請選擇品項</div>
  </div>
</template>
