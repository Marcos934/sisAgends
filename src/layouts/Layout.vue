<template>
  <nav
    class="navbar is-info is-small"
    role="navigation"
    aria-label="main navigation"
  >
    <section class="hero is-info is-small">
      <div class="hero-body">
        <p class="title"><b>Sis</b>Agends</p>
        <p class="subtitle">Agenda de contatos</p>
      </div>
    </section>

   

  </nav>
 <div class="hero-body">
      <div class="container is-max-widescreen">
        <slot> </slot>
      </div>
    </div>
  <section class="hero is-small">
   
    <footer class="footer hero is-medium is-link">
      <div class="content has-text-centered">
        <p>
          Sistema desenvolvido por:
          <strong
            ><a href="https://www.linkedin.com/in/marcosmulinarii/"
              >Marcos V. Mulinari</a
            ></strong
          ><br />
        </p>
      </div>
    </footer>
  </section>
</template>
<script>

export default {};
</script>


<style scoped>
b {
  color: black;
}
</style>