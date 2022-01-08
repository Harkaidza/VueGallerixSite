<template>
    <router-link :to="{name: 'Content', params: {id: product.id}}" class="routerLink">
      <section class="product-item">
        <div>
          <img :src="require(`../assets/images/pictures/${product.id}.jpg`)" alt="image">
        </div>
        <h4>
            <div class = "title">
                «{{ product.title }}»
            </div>

            <div class = "author">
              {{product.author}}
            </div>
        </h4>
        <p>
          {{product.description}}
        </p>
        <div>
          <span class="price">{{ product.price }}$</span>
        </div>
      </section>
    </router-link>
</template>

<script>
export default {
  name: "Product",
  props: ['product']
}
</script>

<style scoped src="../assets/styles/product_style.css">

</style>
