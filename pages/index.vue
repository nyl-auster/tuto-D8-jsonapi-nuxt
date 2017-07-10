<template>
  <section class="recipes">
    <h1>Our latest recipes</h1>
    <div v-for="recipe in recipes">
      <h2> {{recipe.title}} </h2>
      <p> {{recipe.difficulty}} </p>
      <div v-if="recipe.image">
        <img width="300px" :src="recipe.image.thumbnail.filename" />
      </div>
    </div>
  </section>
</template>

<script>

import axios from 'axios'
import jsonapiParser from 'jsonapi-parse'

export default {
  async asyncData () {
    const result = await axios.get('https://dev-contentacms.pantheonsite.io/api/recipes?sort=-created&page[limit]=20&include=image,image.thumbnail&fields[recipes]=image,title,difficulty&fields[files]=filename')
    const recipes = jsonapiParser.parse(result.data).data
    console.log(recipes)
    return { recipes }
  }
}
</script>

