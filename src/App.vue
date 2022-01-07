<template>
  <nav class="navbar navbar-expand navbar-light bg-light">
      <div class="nav navbar-nav">
        <router-link to="/listar" class="nav-link">Contactos</router-link>
        <router-link to="/crear" class="nav-link">Agregar Contacto</router-link>
      </div>
  </nav>
  <br>
  <router-view/>
</template>
