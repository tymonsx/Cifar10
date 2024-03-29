<template>
  <q-page class="flex flex-center">
    <div class="text-h5 text-primary q-ma-sm">Sobre o Aplicativo</div>
    <div style="width: 100%; padding-bottom: 135%;">
      <q-list>
        <q-expansion-item
          group="processo_criacao"
          label="Processo de Criação"
          class="bg-secondary text-justify"
          :default-opened="$q.screen.width > 1000"
          :style="
            $q.screen.width > 1000 ? 'font-size: 18px;' : 'font-size: 16px;'
          "
        >
          <q-card>
            <q-card-section>
              <div class="text-justify">
                <p>
                O aplicativo foi elaborado utilizando as seguintes ferramentas e
                bibliotecas: Python, TensorflowJS, Quasar, VueJS,
                Cordova e Anaconda.
              </p>
              <p>
                A primeira etapa do projeto foi o treinamento da rede neural em
                Python e o salvamento do modelo na extensão H5.
              </p> 
              <p>O próximo passo foi a conversão
                do modelo gerado para JSON através do TensorflowJS Converter
              </p>
              <p>
                A terceira etapa foi a importação do modelo JSON para dentro do TensorflowJS e a integração do mesmo com o framework Quasar
              </p>
              <p>
                Por último, foi gerado um aplicativo para a plataforma Android utilizando a tecnologia Cordova que já vem integrada no framework Quasar
              </p>
              <p>
                O modelo salvo está disponível no link
                <a
                  href="#"
                  v-on:click="
                    abrirLink('https://github.com/tymonsx/cifar10_python')
                  "
                  >Cifar10_Python</a
                >
              </p>
              <p>
                O código do aplicativo está disponível no link
                <a
                  href="#"
                  v-on:click="abrirLink('https://github.com/tymonsx/Cifar10')"
                  >Cifar10</a
                >
              </p>
                <p>
                  Este projeto foi realizado pela equipe de desenvolvimento do Departamento 
                  de Informática em Saúde - EPM - UNIFESP
                  <ul>
                    <li>
                        Antonio Carlos da Silva Junior: Analista de Tecnologia da Informação no Departamento de Informática em Saúde da UNIFESP.
                    </li>
                    <li>
                        Ivan Calixto Ribeiro - Departamento de Informática em Saúde da UNIFESP.  
                    </li>
                    <li>
                        Raphael Hendrigo de Souza Gonçalves: Analista de Tecnologia da Informação no Departamento de Informática em Saúde da UNIFESP.
                    </li>
                  </ul>
                </p>
              </div>
            </q-card-section>
          </q-card>
        </q-expansion-item>
        <q-expansion-item
          group="referencias_utilizadas"
          label="Referências Utilizadas"
          :class="$q.screen.width > 1000 ? 'bg-secondary text-justify' : 'text-justify'"
          :default-opened="$q.screen.width > 1000"
          :style="
            $q.screen.width > 1000 ? 'font-size: 18px;' : 'font-size: 16px;'
          "
        >
          <q-card>
            <q-card-section>
              <div class="text-justify">
                
                <p>
                O App Cifar10 baseia-se no exemplo de técnica de deep learning utilizando rede convolucional apresentado no curso
                <b>Deep Learning Prático com TensorFlow e Python</b>
                disponível na plataforma Udemy através do link  <a
                  href="#"
                  v-on:click="
                    abrirLink(
                      'https://www.udemy.com/course/formacao-deep-learning-tensorflow-python/'
                    )
                  "
                  >Deep Learning Prático com Tensorflow e Python</a
                >
              </p>
              <p>
                As cores, fontes e logos utilizados foram guiados pelo manual da marca da UNIFESP que pode ser acessado pelo link <a
                  href="#"
                  v-on:click="
                    abrirLink(
                      'https://www.unifesp.br/reitoria/dci/images/docs/manual_da_marca/Manual_marca_Unifesp_03-2017.pdf'
                    )
                  "
                  >Manual da Marca</a
                >
              </p>
              </div>
            </q-card-section>
          </q-card>
        </q-expansion-item>
      </q-list>
    </div>
  </q-page>
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
