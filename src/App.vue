<template>
  <div id="app">
    <Header></Header>
    <p>Đây là app đầu tiên</p>
    <Todos/>
    <Footer></Footer>
  </div>
</template>

<script>
import Header from '../src/components/Header';
import Todos from '../src/components/Todos';
import Footer from '../src/components/Footer';
export default {
  name: "App",
  components: {Header,Todos,Footer},
};
</script>

<style>
#app {
  font-family: "Courier New", Courier, monospace;
}
</style>
