<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <FormValidation />
</template>

<script>
import FormValidation from "./components/FormValidation.vue";

export default {
  name: "App",
  components: {
    FormValidation,
  },
};
</script>

<style lang="scss">
:root {
  --primary: #396eb0;
}

html {
  font-size: 62.5%;
}

body {
  box-sizing: border-box;
}

*:focus {
  outline: none;
  box-shadow: 0 0 1rem 0.2rem var(--primary);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
  max-width: 114rem;
  margin: 0 auto;
}

.card {
  max-width: 40rem;
  width: 100%;
  padding: 3.6rem 3.2rem;
  margin: 0 auto;
  background-color: #fff;
  border: 1px solid rgb(240, 240, 240);
  box-shadow: 0 2px 4px rgba(168, 168, 168, 0.43);
  border-radius: 9px;

  & > h1 {
    padding-bottom: 2rem;
  }

  @media (max-width: 480px) {
    max-width: 25rem;
  }
}

.btn {
  &,
  &:link,
  &:visited {
    display: inline-block;
    text-decoration: none;
    padding: 1.4rem 2.4rem;
    border-radius: 9px;
    font-size: 1.6rem;
    font-weight: 600;
    transition: all 0.3s;
  }
}

.invalid {
  color: red;
}

.invalid input {
  border: 1px solid red !important;
}
</style>
