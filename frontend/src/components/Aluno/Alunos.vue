<template>
  <div>
    <Titulo :texto="professorid != undefined ? `Professor: ${Professor.nome}` : 'Alunos'"/>
    <div v-if="professorid">
      <input type="text" placeholder="Nome do Aluno" required v-model="nome" 
        v-on:keyup.enter="addAluno()">
      <button class="btn btnInput" @click="addAluno()">Adicionar</button>
    </div>
    <hr>
    <table>
      <thead>
        <th>Mat.</th>
        <th>Nome</th>
        <th>Sobrenome</th>
        <th>Opções</th>
      </thead>
      <tbody v-if="alunos.length">
        <tr v-for="(aluno, index) in alunos" :key="index">
          <td class="colPequeno">{{ aluno.id }}</td>
          <router-link :to="`/aluno-detalhe/${aluno.id}`" tag="td" style="cursor: pointer;">
            {{ aluno.nome }} 
          </router-link>
          <router-link :to="`/aluno-detalhe/${aluno.id}`" tag="td" style="cursor: pointer;">
            {{ aluno.sobrenome }}
          </router-link>
          <td class="colPequeno">
            <button class="btn btn_danger" @click="remover(aluno)">
              Remover
            </button>
          </td>
        </tr>
      </tbody>
      <tfoot v-else>
        Nenhum Aluno Encontrado
      </tfoot>
    </table>
  </div>
</template>

<script>
import Titulo from '../_share/Titulo'

export default {
  components: {
    Titulo
  },
  data () {
    return {
      titulo: 'Aluno',
      nome: '',
      professorid: this.$route.params.prof_id,
      Professor: {},
      alunos: []
    }
  },
  created() {
    let url

    if (this.professorid) {
      this.carregaProfessores()
      url = `http://localhost:3000/alunos?professor.id=${this.professorid}` 
    } else {
      url = 'http://localhost:3000/alunos'
    }

    this.$http
      .get(url)
      .then( res => res.json() )
      .then( alunos => this.alunos = alunos )
  },
  props: {
  },
  methods: {
    addAluno() {
      let _aluno = {
        nome: this.nome,
        sobrenome: '',
        professor: {
          id: this.Professor.id,
          nome: this.Professor.nome
        }
      }

      this.$http
        .post('http://localhost:3000/alunos', _aluno)
        .then( res => res.json() )
        .then( alunoReturn => {
          this.alunos.push(alunoReturn)
          this.nome = ''
        })
    },
    remover(aluno) {
      this.$http
        .delete(`http://localhost:3000/alunos/${aluno.id}`)
        .then( () => {
            let indice = this.alunos.indexOf(aluno)
            this.alunos.splice(indice, 1)
          } 
        )
    },
    carregaProfessores() {
      this.$http
        .get('http://localhost:3000/professores/' + this.professorid)
        .then( res => res.json() )
        .then( professor => {
          this.Professor = professor
        })
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  input, .btnInput {
    border: 0;
    display: inline;
    font-size: 1.3em;
    padding: 20px;
  }

  input { 
    color: #687f7f;
    width: calc(100% - 195px);
  }
  
  .btnInput { 
    background-color: rgb(116, 115, 115); 
    width: 150px; 
  }
  
  .btnInput:hover { 
    border: 0;
    margin: 0;
    padding: 20px;
  }
</style>
