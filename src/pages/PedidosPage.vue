<template>
  <q-page>
    <listado-pedidos @mostrarD="mostrarDatos" v-if="!mostrar"></listado-pedidos>
    <pedido-form-component
      v-if="mostrar"
      :nuevo="false"
      :pedido="pedidoAct"
    ></pedido-form-component>
  </q-page>
</template>

<script>
import ListadoPedidos from "src/components/ListadoPedidos.vue";
import PedidoFormComponent from "src/components/PedidoFormComponent.vue";
import { ref } from "vue";

export default {
  components: { ListadoPedidos, PedidoFormComponent },
  setup() {
    let mostrar = ref(false);
    let pedidoAct = ref(null);
    return {
      mostrar,
      pedidoAct,
      mostrarDatos(pedido) {
        pedidoAct.value = pedido;
        mostrar.value = true;
      },
    };
  },
};
</script>

<style></style>
