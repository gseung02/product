<template>
  <div class="app">
    <NavBar :categories="categories" @selected="selectedCategory"/>
    <!-- <List :products="products" @add-to-cart="addToCart"/> -->
    <List :products="filterProducts" @add-to-cart="addToCart"/>
    <Cart :cart="cartList" @remove-cart-id="removeCart" @clear-cart="clearCart"/>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import {categories, products} from './assets/products.js';
import Cart from './components/Cart.vue';
import List from './components/List.vue';
import NavBar from './components/NavBar.vue';

//장바구니 상태
const cartList = ref([]);
const selectedMenu = ref('');

const addToCart = (list) => {
  //1. list가 된 내용이 cart에 있는지 없는지 확인
  const findItem = cartList.value.find((item)=>{
    return item.id === list.id;
  });
  if(findItem){
    //2. 있으면 수량을 하나 증가
    findItem.count += 1;
  }else{
  //3. 없으면 cart에 추가, 수량 1개 저장
  cartList.value.push({...list, count:1});
  }
  // console.log(cartList.value);
}
const removeCart = (cartID) => {
  //cartList항목이 새로 생성 : cartID가 없는 데이터로
  cartList.value = cartList.value.filter((item)=>{
    return item.id !== cartID; 
  })
}
const clearCart = (value) => {
  if(value){
    cartList.value = [];
  }
}
const selectedCategory = (item) => {
  // console.log(item);
  // if(item === '전체'){
  //   selectedMenu.value = null;
  // }else{
  //   selectedMenu.value = item;
  // }
  selectedMenu.value = item === '전체' ? null : item;
}
const filterProducts = computed(()=>{
  // products: 배열
  // 배열의 리스트 중에서 category === selectedMenu인 애들만
  const item = products.filter((list)=>{
    return list.category === selectedMenu.value
  });
  return selectedMenu.value ? item : products;
});

</script>

<style lang="scss" scoped>

</style>