<script setup>
    definePageMeta({
        layout: "loginlay"
    });
    const { data: allLogin } = await useFetch('http://localhost:8000/usuarios',{
      key: 'usuarioRequest' 
    });

</script>


<template>
    <div>
        <h1>
            Login:
        </h1>
        <h3 >Faça login de usuario abaixo!!</h3>
        <label for="">Email: </label>
        <select v-model="emails">
        <option value=""></option>

        <option v-for="usuarios in allLogin.data" :key="usuarios.id">
            
           {{ usuarios.nome }}

        </option>
        </select>
        <br>
        <br>
        <NuxtLink to="/menu">
        <button v-if="emails  !== ''" @click="realizarAcao ">Login</button>
        </NuxtLink>
        <br>


    </div>
</template>


<script>
export default {
  data() {
    return {
      emails: ''
    };
  }
};
</script>



