<template>
    <div id="nav">
      <nav>
        <router-link to="/">Início</router-link> |
        <router-link to="/about">Sobre</router-link> |
        <router-link to="/warehouses">Galpões</router-link><br />
        <router-link to="/warehouses/new">Cadastrar Galpão</router-link><br />
        <span>{{ username }}</span>
      </nav>
    </div>
</template>

<script>

export default ({
  name: 'Menu',
  props: ['username']
})
</script>
