<template>
  <h1>{{ formatedTitle }}</h1>
  <h2>
    Product's price : {{ price }} € without taxes. {{ priceWithTaxes }} € with
    taxes.
  </h2>
  <h3>Product's description : {{ description }}</h3>
  <br />
  <img class="resizeImage" :src="image" /><br />
</template>

<script>
export default {
  props: {
    title: String,
    price: Number,
    description: String,
    image: String,
  },
  computed: {
    priceWithTaxes() {
      return this.price * 1.2;
    },
    formatedTitle() {
      return (
        this.title.charAt(0).toUpperCase() +
        this.title.slice(1).toLowerCase() +
        " " +
        "©️"
      );
    },
  },
};
</script>

<style scoped>
.resizeImage {
  max-inline-size: 200px;
}
</style>
