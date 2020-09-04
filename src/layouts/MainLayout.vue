<template>
  <q-layout view="hHh lpR fFf">
    <q-header elevated>
      <q-toolbar class="q-my-sm">
        <img
          src="~assets/logo.png"
          alt="Logo Pelagem Gatos"
          id="logoPelagemGatos"
          clickable
          v-ripple
          @click="$router.replace('/')"
          style="width:60px"
        />
        <q-toolbar-title
          id="tituloGeral"
          clickable
          v-ripple
          @click="$router.replace('/')"
        >
          App Pelagem
        </q-toolbar-title>
        <q-btn id="botaoSobre" icon="info" to="/sobre" flat />
      </q-toolbar>
    </q-header>

    <q-footer>
      <q-toolbar>
        <q-toolbar-title>
          <div>
            <img id="logoEpm" src="~assets/logo_epm.png" />
          </div>
          <!--<div
            class="text-right"
          >-->
          <div
            class="desktop-only text-caption text-center float-left"
            style="width:80%"
          >
            Rua Botucatu, 862-Térreo, Vila Clementino, São Paulo (SP). Cep:
            04023-062 - Email: contato@dis.epm.br - CNPJ:60.453.032/0001-74
          </div>
          <img
            id="logoUnifesp"
            class="text-right"
            src="~assets/logo_unifesp.png"
          />
          <!--</div>-->
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
    <q-page-container>
      <router-view :teste="3" />
    </q-page-container>
  </q-layout>
</template>

<script>
//import EssentialLink from "components/EssentialLink.vue";
import Vue from "vue";
import Vuex from "vuex";
Vue.use(Vuex);

export default {
  name: "MainLayout"
};
</script>
