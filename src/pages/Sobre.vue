<template>
  <q-page class="flex flex-center">
    <div class="text-h5 text-primary q-ma-sm">Sobre o Aplicativo</div>
    <div style="width: 100%; padding-bottom: 135%;">
      <q-list>
        <q-expansion-item
            label="Tutorial sobre como bater a foto"
            group="tutorial_bater_foto"
            class="bg-secondary text-justify"
            :default-opened="$q.screen.width > 1000"
          >
          <q-card>
            <q-card-section class="text-dark text-center">
              <p class="text-justify">O gato deve estar enquadrado de corpo inteiro, sozinho e não pode estar de barriga para cima. A foto deve ser feita com iluminação branca. Desta forma, é garantido que todas as características da pelagem sejam capturas na foto sem alteração de cor.</p>
              <exemploFotosCorretas /><br>
              <exemploFotosIncorretas />
            </q-card-section>
          </q-card>
        </q-expansion-item>
        <q-expansion-item label="Processo de criação" group="processo_criacao"
 :class="$q.screen.width > 1000 ? 'bg-secondary text-justify' : 'text-justify'"
          :default-opened="$q.screen.width > 1000">
        <q-card>
          <q-card-section class="text-dark text-justify">
            <p>O AppPelagemGatos consiste em um exemplo de classificação de imagens utilizando rede neural convolucional com transferência de aprendizado (MobileNetV2 - Imagenet).</p>
            <p>
              O aplicativo foi elaborado utilizando as seguintes ferramentas e
              bibliotecas: Python, TensorflowJS, Tensorflow, Quasar, VueJS,
              Cordova e Anaconda.
            </p>
            <p>
              A primeira etapa do projeto foi a construção de 3 robôs para capturar de imagens de gatos utilizando as APIs do Google, Bing e Pixabay, respectivamente.
            </p>
            <p>
              A segunda etapa do projeto foi o treinamento do modelo em
              Python e o salvamento do mesmo utilizando a extensão H5.
            </p>
            <p>O próximo passo foi a conversão
                do modelo gerado para JSON através do TensorflowJS Converter
            </p>
            <p>
                A quarta etapa foi a importação do modelo JSON para dentro do TensorflowJS e a integração do mesmo com o framework Quasar
            </p>
             <p>
                Por último, foi gerado um aplicativo para a plataforma Android utilizando a tecnologia Cordova que já vem integrada no framework Quasar
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
                <li>Ivan Calixto Ribeiro - Departamento de Informática em Saúde da UNIFESP.</li>
                <li>Raphael Hendrigo de Souza Gonçalves: Analista de Tecnologia da Informação no Departamento de Informática em Saúde da UNIFESP.</li>
              </ul>
              Colaboração internacional Trinity College Dublin - Institute of Neuroscience
              <ul>
                <li>Dr. Matheus Cafalchio</li>
              </ul>
            </p>
          </q-card-section>
        </q-card>
      </q-expansion-item>
      <q-expansion-item
        label="Explicação sobre tipos de pelagem"
        group="explicacao_tipos_pelagem"
        class="bg-secondary text-justify"
        :default-opened="$q.screen.width > 1000"
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
      <q-expansion-item label="Links externos" group="links_externos"
 :class="$q.screen.width > 1000 ? 'bg-secondary text-justify' : 'text-justify'"
          :default-opened="$q.screen.width > 1000">
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
                    'http://cedarseed.com/portfolio/housecat-colors/'
                  )
                "
                >Links sobre combinações e tipos de pelagem - Joumana Medlej</a
              >
            </p>
          </q-card-section>
        </q-card>
      </q-expansion-item>
    </q-list>
    </div>
  </q-page>
</template>
<style>
  .exemploFotos {
    width: 200px;
    display: inline-block;
  }
</style>
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
import exemploFotosIncorretas from "components/ExemploFotosIncorretas.vue";
import exemploFotosCorretas from "components/ExemploFotosCorretas.vue";
 
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
    tortoiseShell,
    exemploFotosIncorretas,
    exemploFotosCorretas
  }
};
</script>