<template>
  <nav class="navbar">
    <div class="logo"><a href="/Seakun.id-Tes-Frontend/">Seakun.id</a></div>
    <div class="list-menu">
      <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#news">News</a></li>
        <li class="dropdown">
          <a href="#" class="dropbtn">Dropdown</a>
          <div class="dropdown-content">
            <a href="#">Instagram</a>
            <a href="#">Twitter</a>
            <a href="#">Youtube</a>
          </div>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {};
</script>

<style>
.navbar {
  justify-content: space-between;
  padding: 15px;
}
.logo {
  margin-right: 100px;
}
ul {
  list-style-type: none;
  overflow: hidden;
}
li {
  list-style: none;
  gap: 25px;
}
li a {
  display: inline-block;
}
.dropdown {
  position: relative;
  display: inline-block;
}
</style>
