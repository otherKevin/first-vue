<template>
  <header>
    <input type="text" v-model="mainTitle" />
    <h1>{{ mainTitle }}</h1>
    <h2>{{ tagline }}</h2>
    <button @click="showHide">{{ buttonText }}</button>
  </header>

  <section class="productCreationArea">
    <div class="formArea">
      <form @submit.prevent="createProduct">
        <label for="newTitle"></label>
        <input type="text" name="newTitle" v-model="newTitle" /><br />
        <label for="newPrice"></label>
        <input type="text" name="newPrice" v-model="newPrice" /><br />
        <label for="newDescription"></label>
        <input
          type="text"
          name="newDescription"
          v-model="newDescription"
        /><br />
        <input type="submit" value="Create" />
      </form>
    </div>
    <br />
    <hr />
    <br />
    <div class="previsualize">
      <h3>Your new product :</h3>
      <br />
      <span>Title of your new product : {{ newTitle }}</span
      ><br />
      <span>Your product's price : {{ newPrice }}</span
      ><br />
      <span>It's description : {{ newDescription }}</span
      ><br />
    </div>
  </section>

  <main v-if="buttonText == 'hide'">
    <Product
      v-for="element in productList"
      :key="element.title"
      :title="element.title"
      :price="element.price"
      :description="element.description"
      :image="element.image"
    />
  </main>
</template>

<script>
import Product from "../components/Product.vue";
export default {
  components: {
    Product,
  },
  mounted() {
    this.getData();
  },
  data() {
    return {
      productList: [],
      /* {
          title: "Voiture",
          price: 12,
          description: "C'est un véhicule",
          image: "https://tinyurl.com/f7js9yx",
        },
        {
          title: "Pistache",
          price: 4,
          description: "Ca se mange",
          image: "https://tinyurl.com/ydtdjkxb",
        },
        {
          title: "Tulipe",
          price: 2,
          description: "C'est une fleur",
          image: "https://tinyurl.com/32bajxph",
        },
        {
          title: "Cuir",
          price: 10,
          description: "C'est un matériau de confection",
          image: "https://tinyurl.com/3emsk5zu",
        } */
      tagline: "Voici le slogan ultime de ce site de ouf",
      mainTitle: "Ici le titre de ce super site",
      buttonText: "show",
      newTitle: "",
      newPrice: "",
      newDescription: "",
      arrayLength: null,
    };
  },

  methods: {
    showHide() {
      if (this.buttonText == "hide") {
        this.buttonText = "show";
      } else {
        this.buttonText = "hide";
      }
    },
    createProduct() {
      this.productList.push({
        title: this.newTitle,
        pice: this.newPrice,
        description: this.newDescription,
      });
      this.newTitle = "";
      this.newPrice = "";
      this.newDescription = "";
    },
    async getData() {
      const response = await fetch("https://fakestoreapi.com/products");
      this.productList = await response.json();
    },
  },
  watch: {
    "productList.length"(newLength, oldLength) {
      console.log("There where " + oldLength + " products in the list.");
      console.log("There are now " + newLength + " products in the list.");
    },
  },
};
</script>

<style scoped>
.formArea {
  display: flex;
  flex-direction: column;
}

.previsualize {
  display: flex;
  flex-direction: column;
}
</style>
