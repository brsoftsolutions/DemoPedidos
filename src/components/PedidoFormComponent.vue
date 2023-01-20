<template>
  <q-page class="flex flex-center q-mt-md">
    <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
      <q-input
        filled
        v-model="name"
        label="Nombre"
        hint="Nombre de solicitante"
        lazy-rules
        :rules="[
          (val) => (val && val.length > 0) || 'Por favor ingresa un nombre',
        ]"
      />

      <q-input
        filled
        v-model="domicilio"
        label="Domicilio"
        lazy-rules
        :rules="[
          (val) =>
            (val && val.length > 10) || 'Por favor ingresa un domicilio real',
        ]"
      />

      <q-input
        filled
        type="number"
        v-model="cantidad"
        label="Cantidad"
        lazy-rules
        :rules="[
          (val) =>
            (val !== null && val !== '') || 'Por favor ingresa un cantidad',
          (val) =>
            (val > 0 && val < 100) || 'Por favor ingresa una cantidad real',
        ]"
      />
      <firma-component v-if="!nuevo" />
      <div>
        <q-btn label="Enviar" type="submit" color="primary" />
        <q-btn
          label="Limpiar"
          type="reset"
          color="primary"
          flat
          class="q-ml-sm"
        />
      </div>
    </q-form>
  </q-page>
</template>

<script>
import FirmaComponent from "src/components/FirmaComponent.vue";
import { ref, onMounted } from "vue";
import { useQuasar } from "quasar";

export default {
  components: { FirmaComponent },
  emits: ["guardar"],
  props: {
    nuevo: {
      type: Boolean,
      required: true,
      default: true,
    },
    pedido: {
      type: Object,
      required: false,
      default: null,
    },
  },
  setup(props, { emit }) {
    const $q = useQuasar();

    let name = ref(null);
    let domicilio = ref(null);
    let cantidad = ref(null);

    onMounted(() => {
      if (props.pedido != null) {
        name.value = props.pedido.nombre;
        domicilio.value = props.pedido.domicilio;
        cantidad.value = props.pedido.cantidad;
      }
    });
    return {
      name,
      domicilio,
      cantidad,

      onSubmit() {
        $q.notify("Registrado correctamente");
        emit("guardar", {
          nombre: name.value,
          domicilio: domicilio.value,
          cantidad: cantidad.value,
        });
        name.value = null;
        domicilio.value = null;
        cantidad.value = null;
      },

      onReset() {
        name.value = null;
        domicilio.value = null;
        cantidad.value = null;
      },
    };
  },
};
</script>

<style></style>
