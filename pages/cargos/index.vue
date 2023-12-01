<script setup>
// função useFetch vai chamar o backend como se fosse no Insomnia
    const { data: allcargos } = await useFetch('http://localhost:8000/cargos',{
      key: 'cargosRequest' 
    });
    
    
    
</script>



<template>
    <div>
        <h1>Cargos:</h1>
        <section v-for="cargo in allcargos.data" :key="cargo.id">
            
            <h3>Cargo: {{ cargo.nome }}</h3>
            <h3>Nível de acesso: {{ cargo.nivelAcesso }}</h3>
            
            <br>
            <hr>
            <br>

            
        </section>
        <br><hr>
    </div>
</template>

        
