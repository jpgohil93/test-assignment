<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div v-for="recipe in recipesData" :key="recipe.id" class="premium-recipe col-sm-4 m-2">
          <PremiumRecipeCard :id="recipe" :data="recipe" :energyType="userData.energyUnits" />
        </div>
        </div>
    </div>
  </div>
</template>

<script>
import PremiumRecipeCard from "./components/PremiumRecipeCard.vue";

export default {
  name: "App",
  components: {
    PremiumRecipeCard
  },
  mounted() {
    this.getUserData()
    this.getRecipesData()
    
  },
  methods: {
    getRecipesData: function() {
      fetch("http://localhost:3000/recipes", { method: 'GET' } )
      .then((res) => res.json())
      .then((res) => {
        this.recipesData = res
        console.log("RES::::", res)
      })
    },
    getUserData: function() {
      fetch("http://localhost:3000/user", { method: 'GET' } )
      .then((res) => res.json())
      .then((res) => {
        this.userData = res
        console.log("userData::::", res.energyUnits)
      })
    }
  },

  data: () => ({
    recipes: ["Premium", "recipes", "list", "goes", "here"],
    userData: [],
    recipesData: [],
  })
};
</script>

<style>
#app {
  font-family: "proxima-nova", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<style scoped>
.cm-logo-wrapper {
  margin-bottom: 30px;
}

.cm-logo {
  max-width: 150px;
  height: auto;
}

.cm-container {
  max-width: 960px;
  margin: auto;
}

/** Remove these styles when done */
/* .premium-recipe {
  margin-top: 24px;
  border: 2px dashed red;
  padding: 16px;
  list-style: none;
} */

.premium-recipe {
  width: 314px;
  border-radius: 10px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  text-align: center;
  padding: 0px;
}

.premium-recipe:hover {
  width: 314px;
  border-radius: 10px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  text-align: center;
  padding: 0px;
  opacity: 0.7;
}

</style>
