<template>
  <div class="flex justify-center items-center p-20">

    <form @submit.prevent="(e) => handleSubmit(e)" class="flex flex-col justify-center items-center gap-2">
      <div class="m-5">
        <h1 class="text-[2.5vh]">Cadastro de Corretor</h1>
      </div>
      <div class="flex space-x-5">
        <input type="text" name="cpf" placeholder="Digite Seu CPF" class="border-2 w-[14vh]">
        <input type="text" name="creci" placeholder="Digite Seu Creci" class="border-2">
      </div>
      <div class="w-[100%]">
        <input type="text" name="name" placeholder="Digite seu nome" class="border-2 w-[100%]">
      </div>
      <button type="submit" class="w-[100%] bg-slate-700 text-white h-6">Enviar</button>
    </form>

  </div>
  
  <div class="flex flex-col justify-center items-center">
    <h2 class="mb-10">Carretores Cadastrados</h2>
      <div class="h-5 w-[70%] grid grid-cols-[5%_40%_20%_20%_15%] self-center [&>*]:flex [&>*]:items-center [&>*]:justify-center [&>*]:ring-2 [&>*]:ring-slate-700">
        <p class="">ID</p>
        <p>Nome</p>
        <p>CPF</p>
        <p>Cresci</p>
        <p>Ação</p>
      </div>
      <div v-for="corretor in corretores" :key="corretores.id" class="grid grid-cols-[5%_40%_20%_20%_15%] [&>*]:p-1 [&>*]:ml-2 [&>*]:border-2 w-[70%] [&>*]:text-[2vh]">
        <div class="">
          <p>{{ corretor.id }}</p>
        </div>
        <div class="">
          <p class="">{{ corretor.name }}</p>
        </div>
        <div class="">
          <p>{{ corretor.cpf }}</p>
        </div>
        <div class="">
          <p>{{ corretor.creci }}</p>
        </div>
        <div class="">
        </div>
      </div>
    </div>
  </template>
  
  <script>
    export default {
      data() {
        return {
            corretores: [],
        }
    },
    methods: {
    async handleSubmit(e) {
      const formData = new FormData(e.target);
      try {
        const res = await fetch("http://127.0.0.1:8000/api/corretor", {
        method: "POST",
        body: formData
      });

      if(res.ok) {
        alert('cadastrado com sucesso!')
        location.reload(); 
        }
      }
      
      catch(err) {
        console.log(err);
      }
    }
  },
    mounted() {
      fetch('http://127.0.0.1:8000/api/corretores')
          .then(api => api.json())
          .then(data => { this.corretores = data });
    }
  }
</script>

<style scoped>
</style>
