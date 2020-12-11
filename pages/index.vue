<template>
  <div class="container">
    <pre><code>{{workshops}}</code></pre>
  </div>
</template>

<script>
import gql from 'graphql-tag'
import {print} from 'graphql/language/printer'

const QUERY = gql`
query MyQuery {
  workshops(order_by: {date: desc}) {
    date
    img
    name
    place
    url
  }
}
`
export default {
  async asyncData ({app}){
    const {data} = await app.$hasura({
      query: print(QUERY)
    })
    return {
      workshops: data.workshops
    }
  }

}
</script>

<style>

</style>