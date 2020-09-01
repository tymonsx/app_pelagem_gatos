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
              <b>Bicolor:</b> geralmente possuem uma cor predominamente branca.
              A cor secundária pode estar presente em formato de manchas
              aleatórias ('magpie'), manchas aleatórias com cauda colorida
              ('harlequin') ou manchas coloridas na cabeça e nas costas (van).
            </p>
            <p>
              <b>Hairless:</b> possuem este nome pela quase completa ausência de
              pelagem.
            </p>
            <p>
              <b>Point color:</b> possuem coloração diferente da cor primária
              somente na cabeça, patas e cauda.
            </p>
            <p>
              <b>Solid color:</b> possuem somente uma cor por toda a sua
              extensão.
            </p>
            <p>
              <b>Tabby classic:</b>possuem listras largas na cor preta e
              geralmente sua cor predominamente é mais clara. Há também a
              presença de uma espécie de 'redemoinho' em sua pelagem.
            </p>
            <p>
              <b>Tabby mackerel:</b> possuem listras verticais e mais finas que
              as do 'tabby classic'. Sua principal característica é um desenho
              em formato de 'M' no meio de sua testa.
            </p>
            <p>
              <b>Tabby spotted:</b> ao invés da presença de listras, ocorre a
              aparição de faixas em formato arredondado.
            </p>
            <p>
              <b>Tortoise shell:</b> possuem esse nome pois sua cor e formato
              assemelham-se com a dos casos de tartarugas. A combinação de cores
              mais comum nesse tipo de gato é a caramelo-preto.
            </p>
            <p>
              <b>Calico:</b> com bastantes semelhanças ao tortoise shell, sua
              principal diferença é a presença da tonalidade branca.
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
