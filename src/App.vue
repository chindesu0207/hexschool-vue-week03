<script setup>
import { ref } from 'vue'
import ProductList from "@/components/ProductList.vue"
import Cart from "@/components/Cart.vue"
import OrderList from "@/components/OrderList.vue"

const data = ref([
  {
    id: 1,
    name: '珍珠奶茶',
    description: '香濃奶茶搭配QQ珍珠',
    price: 50
  },
  {
    id: 2,
    name: '冬瓜檸檬',
    description: '清新冬瓜配上新鮮檸檬',
    price: 45
  },
  {
    id: 3,
    name: '翡翠檸檬',
    description: '綠茶與檸檬的完美結合',
    price: 55
  },
  {
    id: 4,
    name: '四季春茶',
    description: '香醇四季春茶，回甘無比',
    price: 45
  },
  {
    id: 5,
    name: '阿薩姆奶茶',
    description: '阿薩姆紅茶搭配香醇鮮奶',
    price: 50
  },
  {
    id: 6,
    name: '檸檬冰茶',
    description: '檸檬與冰茶的清新組合',
    price: 45
  },
  {
    id: 7,
    name: '芒果綠茶',
    description: '芒果與綠茶的獨特風味',
    price: 55
  },
  {
    id: 8,
    name: '抹茶拿鐵',
    description: '抹茶與鮮奶的絕配',
    price: 60
  }
])

const cart = ref([])
const order = ref([])

const addItem = (item) =>{
  const cartIndex = cart.value.findIndex((product) => product.name === item.name)
  if (cartIndex === -1) {
    const index = data.value.findIndex((product) => product.id === item.id)
    cart.value.push(Object.assign(data.value[index], { count: 1 }))
  } else {
    if(cart.value[cartIndex].count<10){
      cart.value[cartIndex].count++
    }
  }
}

const deleteItem = (index) => {
  cart.value.splice(index, index == 0 ? 1 : index)
}

const createOrder = (total, note) => {
  order.value.push(
    Object.assign(cart.value, { note: note ? note : '無', total: total })
  )
  cart.value = []
}
</script>

<template>
  <div id="root">
    <div class="container mt-5">
      <div class="row">
        <ProductList :data="data" @addItem="addItem"/>
        <Cart :cart="cart" @deleteItem="deleteItem" @createOrder="createOrder"/>
      </div>
      <hr />
      <OrderList :order="order"/>
    </div>
  </div>
</template>
