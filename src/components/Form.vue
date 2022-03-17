<template>
  <v-row justify="center">
    <v-col sm="12" md="10">
      <v-card dark>
        <v-card-text>
          <h1>Novo Galpão</h1>
          <div>{{ msg }}</div>
          <v-form v-on:submit.prevent="postWarehouse()">
            <v-text-field v-model="form.name" label="Nome"></v-text-field>
            <v-text-field v-model="form.code" label="Código"></v-text-field>
            <v-text-field v-model="form.description" label="Descrição"></v-text-field>
            <v-text-field v-model="form.address" label="Endereço"></v-text-field>
            <v-text-field v-model="form.city" label="Cidade"></v-text-field>
            <v-text-field v-model="form.state" label="Estado"></v-text-field>
            <v-text-field v-model="form.postal_code" label="CEP"></v-text-field>
            <v-text-field v-model="form.total_area" label="Área Total"></v-text-field>
            <v-text-field v-model="form.useful_area" label="Área Disponível"></v-text-field>
              <v-btn color="primary" fab right absolute type="submit">
                <v-icon>mdi-content-save</v-icon>
              </v-btn>
          </v-form>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
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
          const response = await this.$http.post("http://localhost:3000/api/v1/warehouses", {
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
          const warehouse = await response.json();

          this.msg = "Galpão cadastrado!";

          this.form = {};
          this.classe = "success";
          this.$emit("sendWarehouse", warehouse);
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