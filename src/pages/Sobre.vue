<template>
  <q-layout
    class="layoutPaginaSobre"
    style="min-width:360px; max-width:800px; width:80%; margin:auto"
  >
    <q-list id="listaSobre">
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
              partir das APIs do Google Search, Bing e Pixabay assim como a base de imagens de raças de cães e gatos de Oxford. 
              Ao final, foi realizada a revisão e seleção das imagens coletadas
              através das APIs, para remover imagens com problemas ou que estejam em categorias incorretas.
            </p>
            <p>
              A segunda etapa do projeto foi o treinamento da rede neural em
              Python utilizando o Tensorflow com um processo de tranferência de apresendizado utilizando como base a 
              MobileNet v2. O próximo passo foi a conversão do modelo gerado no
              formato H5 para os formatos "JSON" e ".bin" (comando
              <b>"tensorflowjs_wizard"</b> no Python). Por último, foi criado
              um aplicativo para android utilizando as tecnologias VueJS, Quasar e Cordova.
            </p>
            <p>
              O treino da rede e o modelo salvo estão disponíveis em: 
              <a
                href="#"
                v-on:click="
                  abrirLink('https://github.com/tymonsx/pelagem_gatos')
                "
                >https://github.com/tymonsx/pelagem_gatos</a
              >
            </p>
            <p>
              O projeto de desenvolvimento do app no Quasar está disponível através do
              seguinte link:
              <a
                href="#"
                v-on:click="
                  abrirLink('https://github.com/tymonsx/app_pelagem_gatos')
                "
                >https://github.com/tymonsx/app_pelagem_gatos</a
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
             Este projeto foi realizado pela equipe de desenvolvimento do Departamento de Informática em Saúde - EPM - UNIFESP
              <ul>
                <li>Antonio Carlos da Silva Junior: Analista de Tecnologia da Informação no Departamento de Informática em Saúde da UNIFESP.</li>
                <li>Raphael Hendrigo de Souza Gonçalves: Analista de Tecnologia da Informação no Departamento de Informática em Saúde da UNIFESP.</li>
                <li>Ivan Calixto Ribeiro: Técnico de Tecnologia da Informação no Departamento de Informática em Saúde da UNIFESP.</li>
              </ul>
              Colaboração internacional Trinity College Dublin - Institute of Neuroscience
              <ul>
                <li>Dr. Matheus Cafalchio</li>
              </ul>
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
      <q-expansion-item
        label="Explicação sobre tipos de pelagem"
        group="sobre"
        class="bg-secondary"
      >
        <q-card>
          <q-card-section class="text-dark text-center">
            <tabbySpotted />
            <tabbyMackerel />
            <tabbyClassic />
            <solidColor />
            <pointColor />
            <hairless />
            <bicolor />
            <calico />
            <tortoiseShell />
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
