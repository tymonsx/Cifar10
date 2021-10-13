<template>
  <q-page class="flex flex-center">
    <div class="q-pl-sm q-pr-sm text-center">
      Categorias aceitas: "AVIÃO", "CARRO", "PÁSSARO", "GATO", "CERVO",
      "CACHORRO", "SAPO", "CAVALO", "BARCO", "CAMINHÃO"
    </div>
    <div class="full-width row flex flex-center">
      <img
        class="col-xs-6 col-sm-3 col-md-2 col-lg-2 col-xl-2"
        id="imagem"
        :src="img"
      />
    </div>
    <q-form @submit.stop="predizerImagem" @reset="limparCampos">
      <div style="width:224px; margin-right: auto; margin-left: auto;">
        <q-file
          outlined
          v-model="arquivo"
          @input="carregarImagem"
          :rules="[val => (val != '' && val != null) || 'Insira uma imagem']"
          accept=".jpg, image/*"
        >
          <template v-slot:prepend>
            <q-icon name="attach_file"></q-icon>
          </template>
        </q-file>
      </div>
      <div class="full-width text-center text-h6 text-primary">
        {{ msgPredicao }}
      </div>
      <div class="full-width text-center q-gutter-sm q-mt-xs">
        <q-btn color="primary" type="submit">Reconhecer</q-btn>
        <q-btn color="primary" type="reset">Limpar Campos</q-btn>
      </div>
    </q-form>
  </q-page>
</template>
<script>
import * as tf from "@tensorflow/tfjs";
import { fetch as fetchPolyfill } from "whatwg-fetch";
import logo from "assets/logo_olho.png";
export default {
  data() {
    return {
      msgPredicao: "Modelo carregado",
      objetoPredicao: "",
      modelo: tf.sequential(),
      arquivo: null,
      img: logo,
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
      this.msgPredicao = "Clique em Reconhecer imagem";
    },
    alertaCarregando(param) {
      if (param == true) {
        //console.log(param);
        this.$q.loading.show({
          spinnerColor: "primary",
          spinnerSize: 140,
          backgroundColor: "white",
          message: "Carregando... Por favor aguarde",
          messageColor: "black"
        });
      } else if (param == false) {
        this.$q.loading.hide();
        //console.log(param);
      }
    },
    predizerImagem() {
      this.alertaCarregando(true);

      this.objetoPredicao = document.getElementById("imagem");
      let arrInput = tf.browser.fromPixels(this.objetoPredicao);
      this.objetoPredicao = tf.image
        .resizeBilinear(arrInput, [32, 32])
        .reshape([1, 32, 32, 3]);

      setTimeout(() => {
        let valor = "";
        try {
          valor = this.modelo.predict(this.objetoPredicao);
        } catch (error) {
          alert(error);
        }
        this.msgPredicao =
          "RESULTADO: " + this.labels[valor.argMax(-1).dataSync()[0]];

        this.alertaCarregando(false);
      }, 500);
    },
    limparCampos() {
      this.arquivo = null;
      this.msgPredicao = "Modelo carregado";
      this.img = logo;
    }
  }
};
</script>
