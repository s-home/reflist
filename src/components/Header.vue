<template>
  <header>
    <a href="https://reflist.netlify.com/" class="home">Home</a>
    <a href="#" class="about">About</a>
    <a href="mailto:reflist@via.tokyo.jp">reflist@via.tokyo.jp</a><span class="contact_span">←お問い合わせ</span>
    <span class="version_span">ver 1.1 </span>
  </header>
</template>

<style scoped>

  header {
    background-color: paleturquoise;
    padding: 20px;
  }

  header a {
    color: coral;
    text-decoration: none;
    background-color: paleturquoise;
    transition: 0.5s;
    margin: 0 15px;
  }

  header a:hover {
    color: orangered;
  }

  .about {
    text-decoration: line-through black;
  }

  .contact_span {
    color: dimgray;
    background-color: paleturquoise;
  }

  .version_span {
    float: right;
    color: dimgray;
    background-color: paleturquoise;
  }

  @media screen and (max-width: 479px) {
    header {
      padding: 15px 3px;
    }
    header a {
      margin: 0 10px;
    }
    header span {
      display: none;
    }
  }

</style>
