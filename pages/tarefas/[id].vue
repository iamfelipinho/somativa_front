<script setup>
    // let imagemDinas = ['https://classic.exame.com/wp-content/uploads/2023/02/neymar-samba-gold.jpg?quality=70&strip=info&w=1024',
    // 'https://avatars.githubusercontent.com/u/89030432?v=4','https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR0fA2dklh3PFLPpqzmfOqBJ4YKRya8DyHEbQ&usqp=CAU'];


    // acessamos o mecanismo de rotas do NUXT
    const route = useRoute();
    const {data: tarefaFound} = await useFetch(`http://localhost:8000/tarefas/${route.params.id}`,{
      key: 'tarefaRequest' 
    });

    const {data: sttsFound} = await useFetch(`http://localhost:8000/tarefasStatus`,{
      key: 'tarefasttsRequest' 
    });
    const paramsID = await route.params.id
    
</script>

<template>
    <div>
      <h1>
        Tarefa: {{ tarefaFound.data.nome}}</h1>
        <br>
        <section>
            <h3>Status: {{ tarefaFound.data.idStatusFK.nome }}</h3>
            <h3>Ambiente: {{ tarefaFound.data.idAmbienteFK.nome }}</h3>
            <h3>Prazo: {{ tarefaFound.data.prazo }}</h3>
        </section>
        <section v-if="mostrar">
            <h3>Data de início: {{ tarefaFound.data.dataInicio }}</h3>
            <h3>Data término: {{ tarefaFound.data.dataFim }}</h3>
            <h3>Descrição: {{ tarefaFound.data.descricao }}</h3>
            <h3>Solicitante: {{ tarefaFound.data.idSolicitanteFK.nome }}</h3>
            <img :src="tarefaFound.data.idSolicitanteFK.image" alt="Imagem do solicitante">
            <p>Imagem do solicitante: {{ tarefaFound.data.idSolicitanteFK.nome }}</p>


            <section v-for="stts in sttsFound.data" :key="stts.id"> 
               
              <h4 v-if="stts.idTarefaFK == paramsID">Nome: {{ stts.idStatusFK.nome }} / Data: {{ stts.data }} / Descrição: {{ stts.descricao }}</h4>
            </section>
           
        </section>
        <br>
        <label for="detalhes">Exibir detalhes? </label>
   
   <button @click="exibirDescricao">Exibir</button>

    <p v-if="mostrar">Detalhes da tarefa</p>

    <br>
    <br>
    
    
    <br>
        <NuxtLink :to="`/tarefas`">
                <button>Voltar a lista de tarefas</button>
            </NuxtLink>
        <br>
        <hr>
    </div>

</template>


<script>
export default {
  data() {
    return {
      mostrar: false 
    };
  },
  methods: {
    exibirDescricao() {
      this.mostrar = true;
    }
  }
};
</script>