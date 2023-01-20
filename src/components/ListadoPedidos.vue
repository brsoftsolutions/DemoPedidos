<template>
  <div>
    <q-list>
      <div>
        <q-item
          @click="mostrar(pedido)"
          clickable
          v-ripple
          v-for="pedido in pedidos"
          :key="pedido.id"
        >
          <q-item-section>
            <q-item-label>Pedido #{{ pedido.id }}</q-item-label>
            <q-item-label caption lines="2">{{ pedido.nombre }}</q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min ago</q-item-label>
            <q-icon name="preview" />
          </q-item-section>
        </q-item>
        <q-separator spaced inset />
      </div>
    </q-list>
  </div>
</template>

<script>
import { useQuasar } from "quasar";
import { ref } from "vue";

export default {
  emits: ["mostrarD"],
  setup(props, { emit }) {
    let pedidos = ref(null);
    const $q = useQuasar();

    pedidos.value = $q.localStorage.getItem("pedidos");

    return {
      pedidos,
      mostrar(pedido) {
        emit("mostrarD", pedido);
      },
    };
  },
};
</script>

<style></style>
