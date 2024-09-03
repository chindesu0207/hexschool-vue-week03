<script setup>
import { defineProps } from 'vue'

defineProps(['order'])
</script>

<template>
  <div class="row justify-content-center">
    <div v-if="order.length == 0" class="alert alert-warning text-center" role="alert">
      目前沒有任何訂單
    </div>
    <div class="col-8">
      <div class="card mb-3" v-for="(order, index) in order" :key="index">
        <div class="card-body">
          <div class="card-title">
            <h5>訂單 {{ index + 1 }}</h5>
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">品項</th>
                  <th scope="col">數量</th>
                  <th scope="col">小計</th>
                </tr>
              </thead>
              <tbody v-for="(item, index) in order" :key="index">
                <tr>
                  <td>{{ item.name }}</td>
                  <td>{{ item.count }}</td>
                  <td>{{ item.price * item.count }}</td>
                </tr>
              </tbody>
            </table>
            <div class="text-end">
              備註: <span>{{ order.note }}</span>
            </div>
            <div class="text-end">
              <h5>
                總計: <span>${{ order.total }}</span>
              </h5>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
