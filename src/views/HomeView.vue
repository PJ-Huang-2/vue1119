<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld title="嘿" msg="kdjfijdiji"/>
    <HelloWorld title="嘿嘿" msg="1"/>
    <HelloWorld title="嘿嘿嘿" msg="2"/>
    <HelloWorld title="嘿嘿嘿嘿" msg="3"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  }
}
</script>
