<template>
  <div class="card">
    <p><strong>{{ name }}</strong></p>
    <p>Código: {{ code }}</p>
    <p>CEP: {{ postal_code }}</p>
  </div>
</template>

<script>

  export default{
    props: {
      name: String,
      code: String,
      postal_code: String,
    }
  }

</script>

<style scoped>
  div.card{
    border: solid 1px #6e6e6e;
    border-radius: 1rem;
    padding: 1rem;
    margin: 0.5rem;
  }
</style>