<template>
  <q-layout view="lHh Lpr lFf">
    <q-header reveal bordered class="bg-primary text-white">
      <q-bar class="q-electron-drag electron-only">
        <div>App Pelagem Gatos</div>

        <q-space></q-space>

        <q-btn dense flat icon="minimize" @click="minimize"></q-btn>
        <q-btn dense flat icon="crop_square" @click="maximize"></q-btn>
        <q-btn dense flat icon="close" @click="closeApp"></q-btn>
      </q-bar>
      <q-toolbar>
        <q-toolbar-title
          clickable
          v-ripple
          @click="$router.replace('/')"
          active-class="my-menu-link"
        >
          <div style="width:80px; float:left; ">
            <img
              style="display:block; margin-right:auto;  "
              width="70px"
              src="~assets/logo.png"
            />
          </div>
          <div
            style="width:50%; margin-left:50%; margin-right:50%; word-break: break-all; padding-top: 20px;"
          >
            <span style="font-size:18px;">App Pelagem</span>
            <br />
          </div>
        </q-toolbar-title>
        <q-btn icon="info" to="/sobre" flat />
      </q-toolbar>
    </q-header>
    <q-footer elevated>
      <q-toolbar>
        <q-toolbar-title>
          <div style="min-width:40px;width:10%; float:left; ">
            <img
              style="margin-top: 5px; "
              width="40px"
              src="~assets/logo_epm.png"
            />
          </div>
          <div
            class="desktop-only text-caption text-center float-left gt-sm"
            style="width:80%"
          >
            Rua Botucatu, 862-Térreo, Vila Clementino, São Paulo (SP). Cep:
            04023-062 - Email: contato@dis.epm.br - CNPJ:60.453.032/0001-74
          </div>
          <div
            class="text-right"
            style="min-width:75px; width:10%;float:right;"
          >
            <img
              style="margin-top: 5px; "
              width="75px"
              src="~assets/logo_unifesp.png"
            />
          </div>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>
<script>
import Vue from "vue";
export default {
  name: "MainLayout",
  methods: {
    minimize() {
      if (process.env.MODE === "electron") {
        this.$q.electron.remote.BrowserWindow.getFocusedWindow().minimize();
      }
    },
    maximize() {
      if (process.env.MODE === "electron") {
        const win = this.$q.electron.remote.BrowserWindow.getFocusedWindow();
        if (win.isMaximized()) {
          win.unmaximize();
        } else {
          win.maximize();
        }
      }
    },
    closeApp() {
      if (process.env.MODE === "electron") {
        this.$q.electron.remote.BrowserWindow.getFocusedWindow().close();
      }
    }
  }
};
</script>
