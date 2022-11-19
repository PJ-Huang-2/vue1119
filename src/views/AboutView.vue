<template>
  <div class="about">
    <h1>This is an about page</h1>
    <Button type="text">Text</Button>
    <Button type="primary" ghost>Primary</Button>

  </div>
 <div class="caro">
  <Carousel v-model="value" loop>
      <CarouselItem v-for="item in 3" :key="item">
        <img alt="" :src="require(`@/assets/avatar/img-kaiso0${item}.jpg`)" style="width: 30vw; margin: 10px">
          <!-- <div class="demo-carousel">1</div>-->
      </CarouselItem> 
      <!-- <CarouselItem>
          <div class="demo-carousel">2</div>
      </CarouselItem>
      <CarouselItem>
          <div class="demo-carousel">3</div>
      </CarouselItem>
      <CarouselItem>
          <div class="demo-carousel">4</div>
      </CarouselItem> -->
  </Carousel>
</div>
</template>

<script>
    export default {
        data () {
            return {
                value: 0
            }
        }
    }
</script>

