<template>
  <main>
    <h1>Find the first game in Board Game Geek's ID sequence that you've played.</h1>
    <BggGame :id="id" />
    <nav class="game-nav" aria-label="Game navigation">
      <button @click="prevId" aria-label="Previous game">Prev</button>
      <button @click="nextId" aria-label="Next game">Next</button>
    </nav>
  </main>
</template>

<script>
import BggGame from '@/components/BggGame'

export default {
  name: 'App',
  components: {
    BggGame
  },
  data () {
    return {
      id: 1
    }
  },
  methods: {
    prevId () {
      if (this.id > 1) {
        this.id--
      }
    },
    nextId () {
      this.id++
    }
  }
}
</script>

<style lang="scss">
:root {
  --green: #155c3c;
  --green-light: #9dceba;
}

html {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

a:focus, button:focus, input:focus, textarea:focus, select:focus {
  outline: 1px solid var(--green);
}

a {
  color: var(--green);
  text-decoration: none;

  &:hover {
    text-decoration: underline;
  }
}

.game-nav {
  display: flex;
  align-items: center;
  justify-content: center;

  button {
    font-size: 1rem;
    margin: 0 1rem;
    padding: 0.5rem;
    border: none;
    color: var(--green);
    text-transform: uppercase;
    font-weight: bold;
    background-color: #efefef;
    border-radius: 3px;
    box-shadow: 0 1px 2px gray;
    transition: transform 0.2s, box-shadow 0.2s;

    &:hover, &:focus {
      cursor: pointer;
      box-shadow: 0 3px 2px gray;
      transform: translateY(-1px);
    }

    &:active {
      box-shadow: 0 0 2px gray;
      transform: translateY(1px);
    }
  }
}
</style>
