<!-- This page is what connects the Supabase database to the front end to fetch the products in a vue component -->

<template>
    <div class="products">
      <Product v-for="product in products" :key="product.id" :product-id="product.id" />
    </div>
  </template>
  
  <script>
  import { ref } from 'vue'
  import Product from '../components/ProductDetails.vue'
  import supabase from '../supabase'
  
  export default {
    components: {
      Product
    },
    setup() {
      const products = ref([])
  
      const fetchProducts = async () => {
        const { data, error } = await supabase
          .from('product')
          .select('*')
        if (error) {
          console.log(error)
        } else {
          products.value = data
        }
      }
  
      fetchProducts()
  
      return { products }
    }
  }
  </script>
  