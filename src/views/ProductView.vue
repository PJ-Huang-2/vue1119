<template>
      <div class="wrapper">
        <main>
            <header>
                search: <input type="text" v-model="search"><br>
                $<input type="number" v-model="min">-<input type="number" v-model="max">
            </header>
            <template v-if="load">loading...</template>
            <template v-else>
                <div class="productContainer">
                    <div v-for="(item, index) in product" :key="item.id">
                        <p>{{item.title}}</p>
                        {{parseRating(item.rating)}}
                        <img :src="item.image" v-bind:alt="item.title">
                        <p>{{parsePrice(item.price)}}元</p>
                        <div>
                            <button v-on:click="reduceCount(index, item)">-</button>
                            <input type="number" min="0" v-model="count[index]">
                            <button @click="addCount(index, item)">+</button>
                        </div>
                    </div>
                </div>
            </template>
        </main>
        <aside>
            訂單
            <ul>
                <li v-for="item in order" :key="item.id">
                    {{item.title}}: {{item.count}}
                </li>
            </ul>
            <p>總價：{{total}}元</p>
        </aside>
    </div>
</template>

   <script>
        Vue.createApp({
            data() {
                return {
                    load: false,
                    source: [],
                    // product: [],
                    count: [],
                    sourceCount: 0,
                    order: [],
                    // total: 0,
                    search: '',
                    min: 0,
                    max: 0,
                }
            },
            computed: { //created: Vue實體被建立完
                product() {
                    let cache = this.source
                    if (this.min > 0) { //篩選最小價錢
                        cache = cache.filter(item => {
                            console.log(item)
                            return item.price > this.min
                        })
                    }
                    if (this.max > 0) { //篩選最大價錢
                        cache = cache.filter(item => {
                            return item.price < this.max
                        })
                    }
                    if (this.search !== '') { //篩選相符標題
                        cache = cache.filter(item => {
                            return item.title.includes(this.search)
                        })
                    }
                    return cache

                },
                total() {
                        let total = 0
                        for (const countIndex in this.product) {
                            total += this.count[countIndex] * this.product[countIndex]['price']
                        }
                        return parseInt(total)
                    } 
            
            },
            watch: {
                //監聽data或computed
                total: {
                    handler: function (newVal, oldVal) {
                        if (newVal > 1000) {
                            alert('你要餓死了')
                        }
                    },
                }
            },
            //method 可以帶參數，computed不行
            methods: {
                parseRating(rating) {
                    if (!rating) return null
                    let starStr = ''
                    const star = parseInt(rating.rate)
                    for (let index = 0; index < star; index++) {
                        starStr += '⭐'
                    }
                    return `${starStr}${rating.count}`
                },
                parsePrice(price) {
                    return `TWD ${price * 33}`
                },
                getResource() {
                    this.load = true
                    fetch('https://fakestoreapi.com/products')
                        .then(res => res.json())
                        .then(json => {
                            this.source = json
                            // console.log(json))
                            for (item in this.product) {
                                this.count.push(0)
                            }
                            this.load = false
                            this.sourceCount = this.source.length
                            console.log(this.sourceCount)
                        })

                },
                addCount(index, item) {
                    this.count[index] += 1
                    // const repeatClick = this.order.some(orderItem =>
                    // // 訂單裡面有沒有(orderItem)存在新增的商品(item)
                    // {return orderItem.id === item.id})
                    // console.log(repeatClick);
                    const prodIndex = this.order.findIndex(orderItem =>{
                       return orderItem.id === item.id
                    }) //把現有清單去找參數傳來的清單跟訂單清單一樣的東西
                    // console.log(repeatClick);
                    console.log(prodIndex);
                    if (prodIndex >= 0) {
                         // 如果訂單裡面有這個商品，就將相同id的商品增加數量count
                         // 取訂單商品的順序
                         console.log(this.order[prodIndex]);
                          // 將訂單商品數量+1
                         this.order[prodIndex]['count'] += 1

                    } else {
                        //prodIndex結果會是-1
                        // 如果訂單裡面沒有這個商品，就新增一個訂單商品
                        this.order.push({
                            id: item.id,
                            title: item.title,
                            price: item.price,
                            count: 1 //初始化是1
                        })
                    }
                    // this.sumTotal()
                    this.setStorage()
                },
                reduceCount(index, item) {
                    if (this.count[index] <= 0) return
                    this.count[index] -= 1
                    const prodIndex = this.order.findIndex(orderItem =>{
                       return orderItem.id === item.id
                    })
                    // this.sumTotal()
                    if(prodIndex < 0)return
                    if(this.order[prodIndex]['count'] > 1){
                        //this.order[prodIndex]['count'] =this.order[prodIndex]['count'] - 1
                        this.order[prodIndex]['count'] -= 1
                    }else{
                        this.order.splice(prodIndex, 1);
                    }
                    this.setStorage()
                },
                getStorage(){
                    const data = localStorage.getItem('turtleShop')
                    this.order = JSON.parse(data)
                    this.order = data? data : []

                },
                setStorage(){
                    console.log("有執行")
                    //陣列或物件轉
                    const data = JSON.stringify(this.order)
                    localStorage.setItem('turtleShop', data)
                },
               
            },
            created() {
                // console.log('created' + this.source.length);
                // this.getResource()
            },
            mounted() {
                this.getResource()
                this.setStorage()
                this.sourceCount = this.source.length
                // console.log('mounted'+this.sourceCount);
            },
            beforeUnmount() {
                // alert('beforeUnmount')
                // console.log('beforeUnmount');
            }

            
        }).mount("#app") 
    </script>
