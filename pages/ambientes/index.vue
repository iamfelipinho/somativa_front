<script setup>
    const { data: allAmbientes } = await useFetch('http://localhost:8000/ambientes',{
      key: 'ambienteRequest' 
    });
    let showForm = false;
    const setShowForm = () => {
        showForm = true;
        refreshNuxtData()
    }   

    let name;


     const saveAmbiente = async() => {
        //imprimindo no console do navegador APENAS PARA TESTE
        console.log("nome", name);

        await useFetch('http://localhost:8000/ambientes/',{
            method: 'POST',
        body:
        [{

		    nome: name  
              
        }], key:'ambienteSave'
       
        
         });
         alert("ambiente novo adicionado com sucesso");
     }


</script>


<template>
    <div>
        <h1>
            Bem vindo aos ambientes
        </h1>
        <section v-for="ambiente in allAmbientes.data" :key="ambiente.id">
            
            <h3>{{ ambiente.id}} - Nome: {{ ambiente.nome }}</h3>
            

        </section>
        <hr>
        <label for="add">Adicionar ambiente? </label>
   
   <button @click="setShowForm">SIM</button>

    <section v-if="showForm === true">
        <br>
        <label for="">nome do ambiente: </label> <input type="text" v-model="name"> <br><br>
        <button @click="saveAmbiente">Salvar ambiente</button>
    </section>
  

    <br>
    <br>
    
    
    
        <hr>
    </div>

</template>

