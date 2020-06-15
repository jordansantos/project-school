<template>
  <div>
    <Titulo :texto="`Aluno: ${Aluno.nome} ${Aluno.sobrenome}`" :btnVoltar="!visualizando">
      <button v-show="visualizando" class="btn btn_editar" @click="editarAluno()">Editar</button>
    </titulo>
    <table>
      <tbody>
        <tr>
          <td class="colPequeno">Matrícula:</td>
          <td>
            <label>{{ Aluno.id }}</label>
          </td>
        </tr>
        <tr>
          <td class="colPequeno">Nome:</td>
          <td>
            <label v-if="visualizando">{{ Aluno.nome }}</label>
            <input v-else v-model="Aluno.nome" type="text" />
          </td>
        </tr>
        <tr>
          <td class="colPequeno">Sobrenome:</td>
          <td>
            <label v-if="visualizando">{{ Aluno.sobrenome }}</label>
            <input v-else v-model="Aluno.sobrenome" type="text" />
          </td>
        </tr>
        <tr>
          <td class="colPequeno">Data de Nascimento:</td>
          <td>
            <label v-if="visualizando">{{ Aluno.dataNascimento }}</label>
            <input v-else v-model="Aluno.dataNascimento" type="text" />
          </td>
        </tr>
        <tr>
          <td class="colPequeno">Professor:</td>
          <td>
            <label v-if="visualizando">{{ Aluno.professor.nome }}</label>
            <select v-else v-model="Aluno.professor">
              <option v-for="(professor, index) in Professores" 
              :key="index" :value="professor">
                {{ professor.nome }}
              </option>
            </select>
          </td>
        </tr>
      </tbody>
    </table>

    <div style="margin-top: 10px;">
      <div v-if="!visualizando">
        <button class="btn btn_salvar" @click="salvar(Aluno)">Salvar</button>
        <button class="btn btn_cancelar" @click="cancelar()">Cancelar</button>
      </div>
    </div>
  </div>
</template>

<script>
  import Titulo from '../_share/Titulo'

  export default {
    components: {
      Titulo
    },
    data() {
      return {
        Aluno: {},
        Professores: [],
        visualizando: true
      }
    },
    created() {
      this.$http
        .get(`http://localhost:3000/alunos/${this.$route.params.id}`)
        .then( res => res.json() )
        .then( alunos => this.Aluno = alunos )
      
      this.$http
        .get('http://localhost:3000/professores')
        .then( res => res.json() )
        .then( professor => this.Professores = professor )
    },
    methods: {
      editarAluno() {
        this.visualizando = !this.visualizando
      },
      salvar(_aluno){
        let _alunoEditar = {
          id: _aluno.id,
          nome: _aluno.nome,
          sobrenome: _aluno.sobrenome,
          dataNascimento: _aluno.dataNascimento,
          professor: _aluno.professor
        }

        this.$http
          .put(`http://localhost:3000/alunos/${_alunoEditar.id}`, _alunoEditar)
        
        this.visualizando = !this.visualizando
      },
      cancelar(){
        this.visualizando = !this.visualizando
      }

      /*
      Minha solução desafio.

      editarAluno() {
        document.querySelectorAll('.lbl_aluno').forEach ( el => el.style.display = 'none' )
        document.querySelectorAll('.input_aluno').forEach ( el => el.style.display = 'block' )
      },
      cancelaEdicao() {
        document.querySelectorAll('.lbl_aluno').forEach ( el => el.style.display = 'block' )
        document.querySelectorAll('.input_aluno').forEach ( el => el.style.display = 'none' )
      }
      */
    },
  }
</script>

<style scoped>
  .btn_editar {
    float: right;
    background-color: rgb(76, 186, 249);
  }

  .btn_salvar {
    float: right;
    background-color: rgb(76, 196, 68);
  }

  .btn_cancelar {
    float: left;
    background-color: rgb(249, 186, 92);
  }

  .colPequeno { 
    width: 20%;
  }

  input, select {
    background-color: rgb(245, 245, 245);
    border: 1px solid silver;
    border-radius: 5px;
    font-family: Montserrat;
    font-size: 0.9em;
    margin: 0;
    padding: 5px 10px;
    /*width: 100%;*/
  }

  select {
    /* height: 38px; */
    width: 100%;
  }


  .input_aluno { display: none; }
</style>