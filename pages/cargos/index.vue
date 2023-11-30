<script setup>
// função useFetch vai chamar o backend como se fosse no Insomnia
    const { data: allcargos } = await useFetch('http://localhost:8000/cargos?all',{
      key: 'cargoRequest' 
    });
    
    
    
</script>



<template>
    <div>
        <h1>Bem vindo as nossas cargos</h1>
        <section v-for="cargo in allcargos.data" :key="cargo.id">
            
            <h3>Nome: {{ cargo.nome }}</h3>
            <br>
        </section>
        <br><hr>
    </div>
</template>