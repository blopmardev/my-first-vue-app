<template>
  <NavBar title="Vue App" :links="[
    { label: 'Google', url: 'http://www.google.es' },
    { label: 'Vue', url: 'http://www.vuejs.org' },
  ]" />
  {{ today }}
  <CustomButton>
  </CustomButton>
  <router-view />
  
  <CartProducts v-show="isCartOpen">
  </CartProducts>

</template>

<script lang="ts">
import { defineComponent,
  onBeforeMount,
  onMounted,
  onUnmounted,
  onUpdated } from 'vue';
import NavBar from "./components/NavBar.vue";
import CustomButton from "./components/CustomButton.vue";
import CartProducts from "./components/CartProducts.vue";
import { useCart } from './composables/useCart';
export default defineComponent({
  name: 'AppComponent',
  components: {
    NavBar,
    CustomButton,
    CartProducts,

  },
  setup() {
    console.log("Creamos en el setup");

    onBeforeMount(()=>{
      console.log("onBeforeMount: antes de montar el componente")
    })

    const today = new Date().toDateString()

    onMounted(()=> {
      console.log("onMounted: componente ya montado");
      console.log(today)
    })

    onUpdated(()=> {
      console.log("onUpdated: componente actualizado");
    })

    onUnmounted(()=> {
      console.log("onUnmounted: componente desmontado");
    });

    const { isCartOpen } = useCart() 

    return {
      today,
      useCart,
      isCartOpen
    }
  }
})
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

body {
  background-color: rgb(231, 229, 229);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
