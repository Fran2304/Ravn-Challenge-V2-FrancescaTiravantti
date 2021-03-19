<template>
  <div class="home">
    <ApolloQuery :query="require('../graphql/allUsers.gql')">
        <template v-slot="{ result: { loading, error, data } }">
          <div v-if="loading">Loading...</div>
          <div v-else-if="error">An error occurred</div>
          <div v-else-if="data">
            <div v-for="user in data.allPeople.people" :key="user.id">
                <li>{{ user.name }}</li>
                <p v-if="user.species">{{user.species.name}} from {{user.homeworld.name}}</p>
            </div>
          </div>
        </template>
    </ApolloQuery>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
}
</script>
<style scoped></style>
