<template>

  <div id="app" class="container py-4">
    <div class="row">
      <!-- 商品列表區 -->
      <ProductList :products="products"@add-cart="addCart"></ProductList>

      <!-- 購物車區 -->
      <Cart :carts="carts" @remove-cart="removeCart"></Cart>
      <!-- :carts是 `Cart` 元件的 props 名稱，代表你要傳資料給 Cart元件。後面的 carts是 App.vue 裡定義的資料（ref 陣列），代表購物車的內容。 -->
    </div>

    <!-- 通知元件 -->
    <Notification></Notification>
  </div>
</template>

<script setup>
import ProductList from './components/ProductList.vue'
import Cart from './components/Cart.vue'
import Notification from './components/Notification.vue'
import { ref,provide,reactive } from 'vue'


// 商品資料
const products = ref([
  {
    id: 1,
    name: '耳罩式藍牙耳機',
    description: '舒適配戴，支援降噪技術',
    price: 2490,
    image:
      'https://images.unsplash.com/photo-1546435770-a3e426bf472b?q=80&w=2065&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  },
  {
    id: 4,
    name: '耳罩式彩虹耳機',
    description: '舒適配戴，支援降噪技術',
    price: 1380,
    image:
      'https://images.unsplash.com/photo-1524678606370-a47ad25cb82a?q=80&w=2069&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  },
  {
    id: 5,
    name: '時尚藍牙耳機',
    description: '舒適配戴，支援降噪技術',
    price: 7990,
    image:
      'https://images.unsplash.com/photo-1628116709703-c1c9ad550d36?q=80&w=2071&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  },
  {
    id: 2,
    name: '機械式鍵盤',
    description: '紅軸機械鍵盤，打字手感極佳',
    price: 1890,
    image:
      'https://images.unsplash.com/photo-1595044426077-d36d9236d54a?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  },
  {
    id: 3,
    name: '無線滑鼠',
    description: '靜音按鍵設計，長效電池',
    price: 890,
    image:
      'https://images.unsplash.com/photo-1527814050087-3793815479db?q=80&w=1928&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  },
])
const carts = ref([
  {
    id: 3,
    name: '無線滑鼠',
    description: '靜音按鍵設計，長效電池',
    price: 890,
    quantity: 2,
    image:
      'https://images.unsplash.com/photo-1527814050087-3793815479db?q=80&w=1928&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D',
  },

])

const addCart =(product) => {
  // console.log("收到子元件傳來的資料:", product);
  const existProduct = carts.value.find(c => c.id === product.id)
  if (existProduct) {
    existProduct.quantity ++
  }else{
    carts.value.push({
      ...product, // 展開運算子，將 product 物件的所有屬性展開並複製到新物件中
      quantity: 1
    })
  }
}

const removeCart = (item) => {
// console.log("移除商品ID:", productId)
// 課程方法
// const index = carts.value.findIndex(c => c.id === productId)
// if (index !== -1) {
//   carts.value.splice(index, 1) // 從陣列中移除該商品
// }
carts.value = carts.value.filter(c => c.id !== item.id)
//c.id !== item.id 代表把不等於 item.id 的商品留下來，等於的商品移除掉
// 若購物車有ABC 三樣商品，點擊移除B，最後會回傳一個新陣列，裡面只會有AC兩樣商品
}
// 通知系統 (使用 provide/inject)
const notificationState = reactive({
  message: 'TTT',
  isShow: false,
})

const showNotification = (message) => {
// console.log('顯示通知:', message)
notificationState.message = message
notificationState.isShow = true
setTimeout(() => {
  notificationState.isShow = false },2000) 
}

provide('notificationState', notificationState)
provide('showNotification', showNotification)
</script>