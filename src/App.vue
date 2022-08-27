<template>
  <header>
    <router-link to="/">
      <h1><span>Vue</span>Movies</h1>
    </router-link>
  </header>

  <main>
    <router-view/>
  </main>
</template>


<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Fira+Sans&display=swap');

* {
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
  margin: 0;
  padding: 0;

  &::selection {
    background: transparentize($color: #e91e63, $amount: 0.5)
  }
}

body { background-color: #262626; }

a { text-decoration: none; }

header {
  display: flex;
  align-items: center;
  justify-content: center;

  background-color: #000;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.1);
  padding: 10px 16px;

  h1 {
    color: #fff;
    font-size: 28px;

    span { color: #e91e63; }
  }
}
</style>
