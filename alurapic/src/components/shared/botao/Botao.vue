<template>
  <button
    @click="disparaAcao()"
    class="botao"
    :class="estiloDoBotao"
    :type="tipo"
  >
    {{ rotulo }}
  </button>
</template>

<script>
export default {
  props: {
    tipo: {
      required: true,
      type: String
    },
    rotulo: {
      required: true,
      type: String
    },
    confirmacao: {
      required: false,
      default: false,
      type: Boolean
    },
    estilo: {
      required: false,
      default: 'padrao',
      type: String
    }
  },
  methods: {
    disparaAcao() {
      if (this.confirmacao) {
      if (this.confirmacao) {
        if (confirm('Confirma operação?')) {
          this.$emit('botaoAtivado');
        }

        return;
      }

      this.$emit('botaoAtivado');
    }
  },
  computed: {
    estiloDoBotao() {
      if (this.estilo == 'perigo') {
        return 'botao-perigo';
      }
      
      return 'botao-padrao';
    }
  }
}
</script>
<style>
  .botao {
    display: inline-block;
    padding: 10px;
    border-radius: 3px;
    margin: 10px;
    font-size: 1.2em;
  }

  .botao-perigo {
    background: firebrick;
    color: white;
  }

  .botao-padrao {
    background: darkcyan;
    color: white;
  }
</style>