<template>
  <div class="col-md-8">
    <h2 class="mb-3">商品列表</h2>
    <div class="row">
      <div v-for="product in products" :key="product.id" class="col-md-4 mb-4">
        <!-- products代表傳進來的商品資料陣列。product代表這一次回圈的商品物件 -->
        <div class="card h-100">
          <img :src="product.image" alt="product.name" class="card-img-top">
          <div class="card-body">
            <h5 class="card-title">{{ product.name }}</h5>
            <p class="card-text">{{ product.description }}</p>
            <p class="fw-bold text-primary">$ {{ product.price }}</p>
            <button class="btn btn-success w-100" @click="handleAddCart(product)"> 加入購物車 </button>
          </div>
        </div>
      </div>
    </div>
  </div>
  <!-- {{ products }} -->
</template>

<script setup>
import { defineProps, defineEmits, inject } from 'vue'

const props = defineProps({
  products: {
    type: Array,
    required: true,
  },
})
const emit = defineEmits(['add-cart'])  

const handleAddCart = (product) => {
  emit('add-cart', product)  // 將商品物件傳給父元件
  showNotification(`商品 ${product.name}已加入購物車`) // 顯示通知
}

const showNotification = inject('showNotification') 
// 注入通知方法
</script>