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
              O logo presente no canto superior esquerdo do aplicativo está
              disponível no site <b>Freepik</b> através dos links
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
            <p>O projeto do robô de captura de imagens está disponível no link: 
              <a
                href="#"
                v-on:click="
                  abrirLink('https://github.com/tymonsx/Robo-Imagens-Gatos')
                "
                >Robô Imagens Gatos</a
              >
            <p>
              A segunda etapa do projeto foi o treinamento da rede neural em
              Python utilizando o Tensorflow; a rede neural utilizada foi a
              MobileNet v2.
            </p>
            <p>
              O próximo passo foi a conversão do modelo gerado no
              formato H5 para os formatos "JSON" e ".bin" (comando
              <b>"tensorflowjs_wizard"</b> no Anaconda)
            </p>
             <p>
              O modelo salvo em formato h5 está disponível para consulta através
              do seguinte link:
              <a
                href="#"
                v-on:click="
                  abrirLink('https://github.com/tymonsx/pelagem_gatos')
                "
                >Modelo H5</a
              >
            </p>
            <p>Por último, foi criado um aplicativo utilizando as tecnologias VueJS, Quasar e Cordova.</p>
            <p>O projeto no Quasar está disponível para consulta através do
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
          </q-card-section>
        </q-card>
      </q-expansion-item>
      <q-expansion-item
        label="Explicação sobre tipos de pelagem"
        group="sobre"
        class="bg-secondary"
      >
        <q-card>
          <q-card-section class="text-dark text-justify">
            <p>
              Este aplicativo possui a capacidade de identificar 9 tipos de
              pelagens diferentes. Segue abaixo uma breve explicação sobre cada
              uma delas.
            </p>
            <p>
              <bicolor />
              <hairless />
              <pointColor />
              <solidColor />
              <tabbyClassic />
              <tabbyMackerel />
              <tabbySpotted/>
              <tortoiseShell />
              <calico />
            </p>
          </q-card-section>
        </q-card>
      </q-expansion-item>
      <q-expansion-item label="Links externos" group="sobre">
        <q-card>
          <q-card-section class="text-dark text-justify">
            <p>
              <a
                href="#"
                v-on:click="
                  abrirLink('https://keras.io/api/applications/mobilenet/')
                "
                >Documentação MobileNet V2</a
              >
            </p>
            <p>
              <a
                href="#"
                v-on:click="
                  abrirLink(
                    'https://www.kaggle.com/zippyz/cats-and-dogs-breeds-classification-oxford-dataset'
                  )
                "
                >Dataset de raças de gatos e cachorros - Oxford</a
              >
            </p>
            <p>
              <a
                href="#"
                v-on:click="
                  abrirLink(
                    'https://meowbarkers.wordpress.com/2015/08/30/tabby-patterns-and-colors-cats/'
                  )
                "
                >Links sobre padrões e cores dos gatos "tabby"</a
              >
            </p>
            <p>
              <a
                href="#"
                v-on:click="
                  abrirLink(
                    'https://www.omlet.us/guide/cats/choosing_the_right_cat_for_you/cat_coat_types'
                  )
                "
                >Links sobre tipos de pelagens de gatos</a
              >
            </p>
            <p>
              <a
                href="#"
                v-on:click="
                  abrirLink(
                    'https://silvershorthairs.com/2017/09/23/featured-content/'
                  )
                "
                >Links sobre tipos de gatos "tabby"</a
              >
            </p>
            <p>
              <a
                href="#"
                v-on:click="
                  abrirLink(
                    'https://commons.wikimedia.org/wiki/File:Cat_pattern_-_Bicolor_(french).svg'
                  )
                "
                >Links sobre tipos de gatos "bicolor"</a
              >
            </p>
            <p>
              <a
                href="#"
                v-on:click="
                  abrirLink('https://github.com/tymonsx/Robo-Imagens-Gatos')
                "
                >Github - Robô Imagens Gatos</a
              >
            </p>
            <p>
              <a
                href="#"
                v-on:click="
                  abrirLink('https://github.com/tymonsx/pelagem_gatos')
                "
                >Github - Modelo Pelagem Gatos</a
              >
            </p>
            <p>
              <a
                href="#"
                v-on:click="
                  abrirLink('https://github.com/tymonsx/app_pelagem_gatos')
                "
                >Github - App Pelagem Gatos</a
              >
            </p>
          </q-card-section>
        </q-card>
      </q-expansion-item>
    </q-list>
  </q-layout>
</template>

<script>
import { openURL } from "quasar";
import tabbySpotted from "components/TabbySpotted.vue";
import tabbyMackerel from "components/TabbyMackerel.vue";
import tabbyClassic from "components/TabbyClassic.vue";
import solidColor from "components/SolidColor.vue";
import pointColor from "components/PointColor.vue";
import hairless from "components/Hairless.vue";
import bicolor from "components/Bicolor.vue";
import calico from "components/Calico.vue";
import tortoiseShell from "components/TortoiseShell.vue";

export default {
  name: "Sobre",

  methods: {
    abrirLink(url) {
      openURL(url);
    }
  },
  components: {
    tabbySpotted,
    tabbyMackerel,
    tabbyClassic,
    solidColor,
    pointColor,
    hairless,
    bicolor,
    calico,
    tortoiseShell
  }
};
</script>
