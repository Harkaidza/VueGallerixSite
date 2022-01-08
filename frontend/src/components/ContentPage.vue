<template>
<section class="content">
<Header></Header>
  <main class ="container" v-if = "product">
    <div class="product-title">
      <h1>{{ product.title }}</h1>
    </div>

    <div class = "info">
      <div class="product-image">
        <img :src="require(`../assets/images/pictures/${product.id}.jpg`)"  class="picture-img-cover" alt="Картина">
      </div>

      <div class ="product-description">
        <div id="year"><h4>Год создания:</h4> {{product.year}} </div>
        <div class="authors"><h4>Автор:</h4> {{ product.author }}</div>
        <div class="genre"><h4>Жанр живописи:</h4> {{ product.genre }}</div>

        <div class = "buying">
          <div class = "buying-price">
            <div class="buying-pricenew-text"><h4>Цена:</h4> {{product.price}}$</div>
          </div>
          <button  class="btn" @click = "addToCart(product)"><span class="text">Добавить <span>в корзину</span></span></button>
          <br><br><br><br>
        </div>
      </div>

      <div class = "product-about">
        <h4>История создания картины:</h4>
        <h5>Автор: {{product.author}}<br>Название: "{{ product.title }}"</h5>
        <div class = "annotation">
          <p>
           {{product.description}}
          </p>
        </div>
      </div>
    </div>

  </main>
  <Footer></Footer>
</section>
</template>

<script>
import Footer from "./Footer";
import Header from "./Header";
import Product from "./Product";

export default {
  name: "ContentPage",
  components: {
    Footer,
    Header,
    Product
  },
    methods: {
      addToCart(product){
          //тут добавление в бд корзины пользователя сделать
          const params = {
              id: product.id, count: 1, userId: localStorage.userId
          }
          this.$http.post('/cart', params)
          //.then(response => product.inCart = response.data.inCart)
      }
    },
  data() {
    return {
      product: null
    }
  },
  created() {
    const id = this.$route.params.id
    this.$http.get('/products/' + id)
      .then(response => this.product = response.data)
  }
}
</script>

<style scoped src="../assets/styles/content-style.css">

</style>
