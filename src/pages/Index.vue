<template>
  <q-page class="flex flex-center">
    <div
      :class="
        $q.screen.width > 1000 ? 'full-width text-center' : ' text-justify'
      "
      :style="
        $q.screen.width > 750
          ? ''
          : 'margin-left: 0.8%; margin-right:0.4%; width:98%;'
      "
    >
      Carregue uma foto das seguintes categorias: "AVIÃO", "CARRO", "PÁSSARO",
      "GATO", "CERVO", "CACHORRO", "SAPO", "CAVALO", "BARCO", "CAMINHÃO"
    </div>
    <div class="full-width text-center q-gutter-xs">
      <img id="imagem" style="width:224px;" :src="img" />
    </div>
    <div class="q-gutter-xs text-center" style="width:224px;">
      <q-file outlined v-model="arquivo" @input="carregarImagem">
        <template v-slot:prepend>
          <q-icon name="attach_file"></q-icon>
        </template>
      </q-file>
    </div>
    <div class="full-width text-center q-gutter-sm">
      <q-btn color="primary" v-on:click="predizerImagem"
        >Reconhecer imagem</q-btn
      >
      <q-btn color="primary" v-on:click="limparCampos">Limpar campos</q-btn>
    </div>
    <div>
      <div class="element q-ma-xs">{{ msgPredicao }}</div>
    </div>
  </q-page>
</template>

<script>
import * as tf from "@tensorflow/tfjs";
import { fetch as fetchPolyfill } from "whatwg-fetch";
import truck from "assets/caminhao.jpg";
export default {
  name: "PageIndex",
  data() {
    return {
      msgPredicao: "Modelo carregado",
      objetoPredicao: "",
      modelo: tf.sequential(),
      arquivo: null,
      img: truck,
      labels: [
        "AVIÃO",
        "CARRO",
        "PÁSSARO",
        "GATO",
        "CERVO",
        "CACHORRO",
        "SAPO",
        "CAVALO",
        "BARCO",
        "CAMINHÃO"
      ]
    };
  },

  mounted() {
    try {
      window.fetch = fetchPolyfill;
      this.carregarModelo();
    } catch (error) {
      alert(error);
    }
  },
  methods: {
    async carregarModelo() {
      try {
        this.modelo = await tf.loadLayersModel("model/model.json");
      } catch (error) {
        alert(error);
      }
    },
    carregarImagem() {
      this.img = URL.createObjectURL(this.arquivo);
      this.msgPredicao = "Clique em reconhecer imagem";
    },
    predizerImagem() {
      this.objetoPredicao = document.getElementById("imagem");
      let arrInput = tf.browser.fromPixels(this.objetoPredicao); //
      this.objetoPredicao = tf.image
        .resizeBilinear(arrInput, [32, 32])
        .reshape([1, 32, 32, 3]);

      let valor = this.modelo.predict(this.objetoPredicao);
      this.msgPredicao = this.labels[valor.argMax(-1).dataSync()[0]];
    },
    limparCampos() {
      this.arquivo = null;
      this.msgPredicao = "Modelo carregado";
      this.img = truck;
    }
  }
};
</script>
