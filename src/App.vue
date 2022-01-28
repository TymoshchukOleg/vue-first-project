<template>
  <div>
    <button @click="clicked += 1">Click me!</button>
    <table>
      <caption><h1>Table</h1>
        {{ showMessage }}
      </caption>
      <thead>
        <tr>
          <th>Active filters are: {{ activeFilters }}</th>
          <th>Products</th>
          <th>Cart</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th><Filters 
          :filters="filters" 
          @changeFilter="onChangeFilter" 
          /></th>
          <th><Products 
          :products="filteredProducts" 
          @addToCart="addToCart"
          @removeFromCart="removeFromCart"
          /></th>
          <th><Cart 
          :cart="cart"
          :products="products"
          /></th>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import Products from './components/Products.vue'
import Filters from './components/Filters.vue'
import Cart from './components/Cart.vue'

export default {
  name: 'App',
  components: {
    Products,
    Filters,
    Cart,
  },
  data() {
    return {
      filters: [
        {
          id: 1,
          title: 'first filter',
        },
        {
          id: 2,
          title: 'second filter',
        },
        {
          id: 3,
          title: 'third filter',
        },
        {
          id: 4,
          title: 'fourth filter',
        },
        {
          id: 5,
          title: 'fifth filter',
        },
        {
          id: 6,
          title: 'sixth filter',
        },
        {
          id: 7,
          title: 'seventh filter',
        },
        {
          id: 8,
          title: 'eighth filter',
        },
        {
          id: 9,
          title: 'ninth filter',
        },{
          id: 10,
          title: 'the tenth filter',
        },
      ],
      products: [
        {
          id: 1,
          name: 'product',
          body: 'description',
          filters: [1,7],
        },
        {
          id: 2,
          name: 'product',
          body: 'description',
          filters: [3,4],
        },
        {
          id: 3,
          name: 'product',
          body: 'description',
          filters: [4,9],
        },
        {
          id: 4,
          name: 'product',
          body: 'description',
          filters: [8,7],
        },
        {
          id: 5,
          name: 'product',
          body: 'description',
          filters: [3,4],
        },
        {
          id: 6,
          name: 'product',
          body: 'description',
          filters: [6,9],
        },
        {
          id: 7,
          name: 'product',
          body: 'description',
          filters: [1,7],
        },
        {
          id: 8,
          name: 'product',
          body: 'description',
          filters: [10,4],
        },
        {
          id: 9,
          name: 'product',
          body: 'description',
          filters: [2,9],
        },
        {
          id: 10,
          name: 'product',
          body: 'description',
          filters: [5,7],
        },
      ],
      cart: [],
      cartID: null,
      activeFilters: [],
      clicked: null,
    }
  },
  methods: {
      onChangeFilter(id, array) {
        this.activeFilters = array;
      },
      addToCart(id) {
        this.cart.push(this.products[id]);
      },
      removeFromCart(id) {
        let deleteFlag = false;

        for(let i = 0; i < this.cart.length; i++) {
          if(this.cart[i].id === id) {
            this.cart.splice(i, 1);
            deleteFlag = true;
          }
          if(deleteFlag) {
            break;
          }
        }
      },
  },
  computed: {
      filteredProducts: function() {
        return this.products.filter((product) => {
          if(this.activeFilters.length == 0){
            return this.products;
          }
          return product.filters.some((elem) => {
            return this.activeFilters.indexOf(elem) >= 0;
          });
        })
      },
      showMessage: function() {
        let msg = localStorage.getItem('say');
        return msg; 
      }
  },
  mounted() {
    localStorage.setItem('say', 'message')
  },
  watch: {
    clicked: {
      handler(val) { 
        if(val) {
          alert(`You have clicked on button: ${val} times`);
        }
      }
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

table {
  margin-left: 150px;
  margin-right: 150px;
  table-layout: fixed;
  width: 80%;
  border-collapse: collapse;
  border: 3px solid black;
}
th, td {
  padding: 15px;
}

.products {
  padding: 10px;
  border: 2px solid black;
  cursor: pointer;
  margin: 5px;
}

</style>
