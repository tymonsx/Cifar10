<template>
  <q-layout class="layoutPaginaSobre">
    <q-list id="listaSobre">
      <q-expansion-item
        label="Fonte do modelo"
        group="sobre"
        class="bg-secondary"
      >
        <q-card>
          <q-card-section class="text-dark text-justify">
            <p>
              O <b>Aplicativo Teste Cifar-10</b> baseia-se no modelo apresentado
              na <b>"Seção 5:Redes neurais convolucionais"</b> do curso
              <b>"Deep Learning Prático com TensorFlow e Python"</b> disponível
              na plataforma Udemy.
            </p>
            <p>
              O curso foi elaborado pelos seguintes professores: Jones Granatyr,
              Dr. Ryan Ahmed, Hadelin de Ponteves, Kirill Eremenko,
              SuperDataScience Team e Mitchell Bouchard.
            </p>
            <p>
              O referido curso está disponível no seguinte link:
              <a
                href="#"
                v-on:click="
                  abrirLink(
                    'https://www.udemy.com/course/formacao-deep-learning-tensorflow-python/'
                  )
                "
                >Deep Learning Prático com Tensorflow e Python</a
              >
            </p>
          </q-card-section>
        </q-card>
      </q-expansion-item>
      <q-expansion-item label="Imagens utilizadas" group="sobre">
        <q-card>
          <q-card-section class="text-dark text-justify">
            <p>
              O conjunto de dados CIFAR-10 é uma coleção de imagens comumente
              usadas para treinar algoritmos de aprendizado de máquina e visão
              computacional. É um dos conjuntos de dados mais usados ​​para
              pesquisa de aprendizado de máquina.
            </p></q-card-section
          >
        </q-card>
      </q-expansion-item>
      <q-expansion-item
        label="Processo de criação"
        group="sobre"
        class="bg-secondary"
      >
        <q-card>
          <q-card-section class="text-dark text-justify">
            <p>
              O aplicativo foi elaborado utilizando as seguintes ferramentas e
              bibliotecas: Python, TensorflowJS, Tensorflow, Quasar, Vue,
              Cordova e Anaconda.
            </p>
            <p>
              A primeira etapa do projeto foi o treinamento da rede neural em
              Python utilizando o Tensorflow. O próximo passo foi a conversão do
              modelo gerado no formato H5 para os formatos "JSON" e ".bin"
              (comando <b>"tensorflowjs_wizard"</b> no Anaconda). Por último,
              foi criado um aplicativo utilizando as tecnologias VueJS, Quasar e
              Cordova.
            </p>
            <p>
              O modelo salvo em formato h5 está disponível para consulta através
              do seguinte link
              <a
                href="#"
                v-on:click="
                  abrirLink('https://github.com/tymonsx/sorvete_python')
                "
                >Modelo H5</a
              >
            </p>
            <p>
              O projeto no Quasar está disponível para consulta através do
              seguinte link:
              <a
                href="#"
                v-on:click="abrirLink('https://github.com/tymonsx/sorvete')"
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
