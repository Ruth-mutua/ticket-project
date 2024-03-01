<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="primary">
      <b-navbar-brand href="#">Admin_01's Dashboard</b-navbar-brand>
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav class="ml-auto">
          <b-breadcrumb>
            <b-breadcrumb-item href="#summary">Summary</b-breadcrumb-item>
            <b-breadcrumb-item href="#logout">Logout</b-breadcrumb-item>
          </b-breadcrumb>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: 'AdminNavBarComponent'
};
</script>

<style scoped>
/* Your component styles */
</style>
