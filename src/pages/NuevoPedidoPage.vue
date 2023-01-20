<template>
  <pedido-form-component
    :nuevo="true"
    @guardar="guardar"
  ></pedido-form-component>
</template>

<script>
import PedidoFormComponent from "src/components/PedidoFormComponent.vue";
import { useQuasar } from "quasar";

export default {
  components: { PedidoFormComponent },
  setup() {
    const $q = useQuasar();

    let pedidos = $q.localStorage.getItem("pedidos");
    // $q.localStorage.set(key, value);
    // const value = $q.localStorage.getItem(key);

    // $q.sessionStorage.set(key, value);
    // const otherValue = $q.sessionStorage.getItem(key);

    return {
      guardar(payload) {
        console.log(pedidos);
        let arr = [];
        if (pedidos != null) {
          arr = pedidos;
          payload.id = pedidos.length + 1;
        } else {
          payload.id = 1;
        }
        arr.push(payload);

        $q.localStorage.set("pedidos", arr);
        pedidos = $q.localStorage.getItem("pedidos");
      },
    };
  },
};
</script>

<style></style>
