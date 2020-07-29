<template>
  <q-layout view="lHh Lpr lFf">
    <q-header reveal bordered class="bg-primary text-white">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img
              src="https://www.unifesp.br/reitoria/dci/images/docs/manual_da_marca/Unifesp_completa_verde_negativo_RGB.png"
            />
          </q-avatar>
          Cifar-10 Desenvolvido pela UNIFESP
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer reveal bordered class="bg-primary text-white">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img
              src="https://www.unifesp.br/reitoria/dci/images/docs/manual_da_marca/Unifesp_completa_verde_negativo_RGB.png"
            />
          </q-avatar>
          Cifar-10 Desenvolvido pela UNIFESP
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
export default {
  name: "MainLayout"
};
</script>
