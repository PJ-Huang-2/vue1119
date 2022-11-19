<template> 
<div class="bg" :style="{
    	backgroundImage: `url( ${ require('@/assets/bc/background3.jpg') } )`
    }"></div>
  <div class="hello"
  >
    <div class="img" v-for="item in 3" :key="item">
      <img alt="" :src="require(`@/assets/avatar/img-kaiso0${item}.jpg`)">
    </div>
   
    
    <div class="item">
      <h1>{{ title }}</h1>
      <h1>{{ msg }}</h1>
      <button>搶票唷</button>
    </div>
   
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    title: String,
    msg: String,
    type: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.hello {
  width: 100%;
  display: inline-block;
}


.img {
  width: 30rem;
  height: 30rem;
  background-color: #ddd;
}
.img img {
  width: 100%;
}
.bg {
  width: 100%;
  height: 100vh;
}
.wide {
  width: 30vw;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
