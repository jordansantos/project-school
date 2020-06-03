<template>
  <div>
    <Titulo texto='Aluno'/>
    <div>
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
          <td>{{ aluno.id }}</td>
          <td>{{ aluno.nome }}</td>
          <td>{{ aluno.sobrenome }}</td>
          <td><button class="btn btn_danger" @click="remover(aluno)">Remover</button></td>
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
      alunos: []
    }
  },
  created() {
    let url = this.professorid ? `http://localhost:3000/alunos?professor.id=${this.professorid}` : 'http://localhost:3000/alunos'
    
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
        sobrenome: ''
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
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  input, .btnInput { border: 0; padding: 20px; font-size: 1.3em; display: inline; }
  input { width: calc(100% - 195px); color: #687f7f; }
  .btnInput { background-color: rgb(116, 115, 115); width: 150px; }
  .btnInput:hover { padding: 20px; margin: 0; border: 0; }
</style>
