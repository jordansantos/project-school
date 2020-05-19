<template>
  <div>
    <Titulo texto='Professor'/>

    <table>
      <thead>
        <th>Mat.</th>
        <th>Nome</th>
        <th>Opções</th>
      </thead>
      <tbody v-if="professores.length">
        <tr v-for="(professor, index) in professores" :key="index">
          <td>{{ professor.id }}</td>
          <td>{{ professor.nome }} {{ professor.sobrenome }}</td>
          <td>Remover</td>
        </tr>
      </tbody>
      <tfoot v-else>
        Nenhum Professor Encontrado
      </tfoot>
    </table>
  </div>
</template>

<script>
  import Titulo from '../_share/Titulo';

  export default {
    components: {
      Titulo
    },
    data() {
      return {
        professores: [
          {id: 1, nome: 'Maria'},
          {id: 2, nome: 'Mariana'},
          {id: 3, nome: 'Marcela'},
        ]
      }
    }
  }
</script>

<style scoped>

</style>