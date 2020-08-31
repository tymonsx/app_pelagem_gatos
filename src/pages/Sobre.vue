<template>
  <q-layout class="layoutPaginaSobre">
    <q-list id="listaSobre">
      <q-expansion-item
        label="Imagens utilizadas"
        group="sobre"
        class="bg-secondary"
      >
        <q-card>
          <q-card-section class="text-dark text-justify">
            <p>
              O logo presente no canto superior direito do aplicativo está
              disponível no site <b>Freepik</b> através do link
              <a
                href="#"
                v-on:click="abrirLink('https://www.freepik.com/vectors/logo')"
                >Logo vector created by freepik - www.freepik.com</a
              >
              e
              <a
                href="#"
                v-on:click="
                  abrirLink(
                    'https://www.freepik.com/free-vector/mascot-logo-with-with-kitten_7088690.htm#page=1&query=cat%20logo&position=6'
                  )
                "
                >Kitten cat logo</a
              >
            </p>
          </q-card-section>
        </q-card>
      </q-expansion-item>
      <q-expansion-item label="Processo de criação" group="sobre">
        <q-card>
          <q-card-section class="text-dark text-justify">
            <p>
              O aplicativo foi elaborado utilizando as seguintes ferramentas e
              bibliotecas: Python, TensorflowJS, Tensorflow, Quasar, Vue,
              Cordova e Anaconda.
            </p>
            <p>
              A primeira etapa do projeto foi a captura de imagens de gatos a
              partir das APIs do Google Search, Bing e Pixabay. Ao final, foi
              realizada a revisão e seleção das melhores imagens coletadas
              através das APIs
            </p>
            <p>
              A segunda etapa do projeto foi o treinamento da rede neural em
              Python utilizando o Tensorflow; a rede neural utilizada foi a
              MobileNet v2. O próximo passo foi a conversão do modelo gerado no
              formato H5 para os formatos "JSON" e ".bin" (comando
              <b>"tensorflowjs_wizard"</b> no Anaconda). Por último, foi criado
              um aplicativo utilizando as tecnologias VueJS, Quasar e Cordova.
            </p>
            <p>
              O modelo salvo em formato h5 está disponível para consulta através
              do seguinte link
              <a
                href="#"
                v-on:click="
                  abrirLink('https://github.com/tymonsx/pelagem_gatos')
                "
                >Modelo H5</a
              >
            </p>
            <p>
              O projeto no Quasar está disponível para consulta através do
              seguinte link:
              <a
                href="#"
                v-on:click="
                  abrirLink('https://github.com/tymonsx/app_pelagem_gatos')
                "
                >Projeto Quasar</a
              >
            </p>
            <p>
              A documentação para geração do aplicativo com o Cordova está
              disponível no seguinte link:
              <a
                href="#"
                v-on:click="
                  abrirLink(
                    'https://quasar.dev/quasar-cli/developing-cordova-apps/preparation'
                  )
                "
                >Developing Cordova Apps - Preparation</a
              >
            </p>
            <p>
              A disponibilização dos arquivos no Github bem como a supervisão e
              elaboração do projeto foram realizadas pelo
              <b>Sr. Antonio Carlos da Silva Júnior</b>, Analista de Tecnologia
              da Informação no Departamento de Informática em Saúde da UNIFESP.
            </p>
            <p>
              A revisão e seleção das imagens coletadas pelas APIs foram
              realizadas pelo <b>Sr. Raphael Hendrigo de Souza Gonçalves</b>,
              Analista de Tecnologia da Informação no Departamento de
              Informática em Saúde da UNIFESP.
            </p>
          </q-card-section>
        </q-card>
      </q-expansion-item>
    </q-list>
  </q-layout>
</template>

<script>
import { openURL } from "quasar";

export default {
  name: "Sobre",

  methods: {
    abrirLink(url) {
      openURL(url);
    }
  }
};
</script>
