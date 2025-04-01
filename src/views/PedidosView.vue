<template>
  <div class="main-container">
    <h1>Gerenciador de pedidos</h1>
    <DashBoard/>
  </div>
</template>

<script>
import DashBoard from '../components/DashBoard.vue';
export default {
  nome: "PedidosView",
  components: {
    DashBoard
  },
}
</script>
