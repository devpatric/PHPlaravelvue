<template>
    <div>
        <h1>Update Item</h1>
        <div class="row">
          <div class="col-md-10"></div>
          <div class="col-md-2"><router-link :to="{ name: 'DisplayItem' }" class="btn btn-success">Return to Items</router-link></div>
        </div>

        <form v-on:submit.prevent="updateItem">
            <div class="form-group">
                <label>Recipe Name</label>
                <input type="text" class="form-control" v-model="recipe.name">
            </div>

            <div class="form-group">
                <label name="product_price">Item Price</label>
                <input type="text" class="form-control" v-model="recipe.Ingredients">
            </div>
<div class="form-group">
                <label name="product_price">Item Directions</label>
                <input type="text" class="form-control" v-model="recipe.Directions">
            </div>
            <div class="form-group">
                <button class="btn btn-primary">Update</button>
            </div>
        </form>
    </div>
</template>

<script>

    export default{
        data(){
            return{
                recipe:{}
            }
        },

        created: function(){
            this.getItem();
        },

        methods: {
            getItem()
            {
              let uri = `http://localhost:8081/recipes/${this.$route.params.id}/edit`;
                this.axios.get(uri).then((response) => {
                    this.recipe = response.data;
                });
            },

            updateItem()
            {
              let uri = 'http://localhost:8081/recipes/'+this.$route.params.id;
                this.axios.put(uri, this.recipe).then((response) => {
                  this.$router.push({name: 'DisplayItem'});
                });
            }
        }
    }
</script>