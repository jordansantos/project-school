<template>
  <div>
    <div class="div_voltar">
      <h2>{{ texto }}</h2>
      <div class="voltar">
        <slot></slot>
        <button v-show="btnVoltar" class="btn btn_voltar" @click="voltar()">Voltar</button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      texto: String,
      btnVoltar: Boolean
    },
    methods: {
      voltar() {
        this.$router.back()
      }
    },
  }
</script>

<style scoped>
  .div_voltar {
    display: flex;
    width: 50%;
  }

  .voltar {
    margin-top: 15px;
    position: absolute;
    width: 50%;
  }

  .btn_voltar {
    background-color: rgb(199, 199, 199);
    float: right;
  }
</style>