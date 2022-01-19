<template>
  <div>
    <h1>Novo Galpão</h1>
    <div>{{ msg }}</div>
    <form v-bind:class="classe" v-on:submit.prevent="postWarehouse()">
      <input v-model="form.name" placeholder="Nome"><br>
      <input v-model="form.code" placeholder="Código"><br>
      <input v-model="form.description" placeholder="Descrição"><br>
      <input v-model="form.address" placeholder="Endereço"><br>
      <input v-model="form.city" placeholder="Cidade"><br>
      <input v-model="form.state" placeholder="Estado"><br>
      <input v-model="form.postal_code" placeholder="CEP"><br>
      <input v-model="form.total_area" placeholder="Área Total"><br>
      <input v-model="form.useful_area" placeholder="Área Disponível"><br>
      <button>Enviar</button>
    </form>
  </div>
</template>

<script>

  export default ({
    name: 'WarehouseForm',
    data() {
      return {
        classe: "",
        msg: null,
        form:{
          name: null,
          code: null,
          description: null,
          address: null,
          city: null,
          state: null,
          postal_code: null,
          total_area: null,
          useful_area: null,
        }
      }
    },
    methods:{
      async postWarehouse(){
        try{
          await this.$http.post("http://localhost:3000/api/v1/warehouses", {
            name: this.form.name,
            code: this.form.code,
            description: this.form.description,
            address: this.form.address,
            city: this.form.city,
            state: this.form.state,
            postal_code: this.form.postal_code,
            total_area: this.form.total_area,
            useful_area: this.form.useful_area,
          });

          this.msg = "Galpão cadastrado!";

          this.form = {};
          this.classe = "success";
        }
        catch(error){
          const error_msg = await error.json();
          this.msg = error_msg;
          this.classe = "error";
        }
      }
    }
  })

</script>

<style scoped>
  form.success input{
    border: 1px solid green;
  }

  form.error input{
    border: 1px solid red;
  }
</style>