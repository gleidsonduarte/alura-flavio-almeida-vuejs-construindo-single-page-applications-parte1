<template>
  <div class="corpo">
    <h1 class="titulo">{{ titulo }}</h1>
    <input
      type="search"
      class="filtro"
      @input="filtro = $event.target.value"
      placeholder="Filtrar por parte do tírulo"
    >
    <ul class="lista-fotos">
      <li class="lista-fotos-item" :key="foto" v-for="foto of fotosComFiltro">
        <meu-painel :titulo="foto.titulo">
          <imagem-responsiva :url="foto.url" :titulo="foto.titulo" />
          <meu-botao
            tipo="button"
            rotulo="REMOVER"
            @botaoAtivado="remove(foto)"
            :confirmacao="true"
            estilo="perigo" />
        </meu-painel>
      </li>
    </ul>
  </div>
</template>

<script>
import Painel from '../shared/painel/Painel.vue';
import ImagemResponsiva from '../shared/imagem-responsiva/ImagemResponsiva.vue';
import Botao from '../shared/botao/Botao.vue';

export default {
  components: {
    'imagem-responsiva': ImagemResponsiva,
    'meu-painel': Painel,
    'meu-botao': Botao
  },
  data() {
    return {
      titulo: 'Cachorro',
      fotos: [],
      filtro: ''
    }
  },
  computed: {
    fotosComFiltro() {
      if (this.filtro) {
        let exp = new RegExp(this.filtro.trim(), 'i');
        return this.fotos.filter(foto => exp.test(foto.titulo));
      } else {
        return this.fotos;
      }
    }
  },
  methods: {
    remove(foto) {
      alert('Remover a foto ' + foto.titulo);
    }
  },
  created() {
    this.$http.get('http://localhost:3000/v1/fotos')
      .then(res => res.json())
      .then(
        fotos  => this.fotos = fotos,
        error => console.log(error)
      );
  }
}
</script>

<style>
  .centralizado {
    text-align: center;
  }

  .lista-fotos {
    list-style: none;
  }

  .lista-fotos .lista-fotos-item {
    display: inline-block;
  }

  .titulo {
    text-align: center;
  }

  .filtro {
    display: block;
    width: 100%;
  }
</style>
