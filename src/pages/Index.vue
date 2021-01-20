<template>
  <q-page class="flex flex-center">
    <div class="full-width text-center">
      Carregue uma foto das seguintes categorias abaixo para reconhecimento:<br />
      "AVIÃO", "CARRO", "PÁSSARO"<br />
      "GATO", "CERVO", "CACHORRO"<br />
      "SAPO", "CAVALO" "BARCO"<br />
      "CAMINHÃO"<br />
    </div>
    <div class="full-width text-center">
      <img style="width:300px;" id="imagem" :src="img" />
    </div>
    <div class="q-gutter-md text-center" style="width:300px;">
      <q-file outlined v-model="file" @input="carregaImagem">
        <template v-slot:prepend>
          <q-icon name="attach_file"></q-icon>
        </template>
      </q-file>
    </div>
    <div class="full-width text-center">
      <q-btn color="primary" v-on:click="predict">Reconhecer imagem</q-btn>
    </div>
    <div>
      <div class="element">{{ msgPredicao }}</div>
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
      msgPredicao: "Clique em Reconhecer imagem",
      valorPredito: "",
      model: tf.sequential(),
      file: null,
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
      this.carregar_modelo();
    } catch (error) {
      alert(error);
    }
    //URL.createObjectURL(file);
  },
  methods: {
    async carregar_modelo() {
      try {
        this.model = await tf.loadLayersModel("model/model.json");
      } catch (error) {
        alert(error);
      }
    },
    carregaImagem() {
      this.img = URL.createObjectURL(this.file);
      console.log(this.file);
      this.msgPredicao = "Clique em Reconhecer imagem";
    },
    predict() {
      this.valorPredito = document.getElementById("imagem");
      let arrInput = tf.browser.fromPixels(this.valorPredito); //
      this.valorPredito  = tf.image
        .resizeBilinear(arrInput, [32, 32])
        .reshape([1, 32, 32, 3]);

      let valor = this.model.predict(this.valorPredito);
      this.msgPredicao = this.labels[valor.argMax(-1).dataSync()[0]];
    }
  }
};
</script>
