<template>
  <div class="news">
    <h1>This is an about page</h1>
    <HelloWorld title="緊張" type="wide"/>
    <images Link="https://fakeimg.pl/100/"/>
    <button type="primary">AAAA</button>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Images from '@/components/Images.vue'


export default {
  name: 'NewsView',
  components: {
    HelloWorld,
    Images,

  }
}
</script>
