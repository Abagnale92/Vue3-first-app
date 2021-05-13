<template>
  
  <header>
    <router-link to="/">
      <h1><span> Vue</span>Films</h1>
    </router-link>
  </header>
  
  <main>
    <router-view/>
  </main>

<footer>
  <p>Created by Giuseppe</p>
</footer>
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Courier New', Courier, monospace;

  &::selection {
    background: transparentize($color: #42b883, $amount: 0.5)
  }

  body{
    background-color: #35462F; 
  }

  a{
    text-decoration: none;
  }

  header {
    display: flex;
    align-items: center;
    justify-content:center;
    padding: 5px 16px;
    background-color:yellowgreen;
    box-shadow: 0px 0px 6px rgba($color: white, $alpha: 0.1);

    h1 {
      color: white;
    }

    span{
      color: blueviolet;
    }

  }
footer {
    position:fixed;
    left: 0;
    bottom: 0;
    padding:5px 16px;
    width: 100%;
    background-color:yellowgreen;
    color: white;
    text-align: center;

  }

}
</style>
