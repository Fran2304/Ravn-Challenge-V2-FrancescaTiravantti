<template>
  <div class="home">
    <ApolloQuery :query="require('../graphql/allUsers.gql')">
      <template v-slot="{ result: { loading, error, data } }">
        <section v-if="loading">Loading...</section>
        <section v-else-if="error">An error occurred</section>
        <section v-else-if="data">
          <section v-for="user in data.allPeople.people" :key="user.id">
            <RouterLink :to="`character/${user.id}`" class="link-character">
              <section class="container-character">
                <h4>{{ user.name }}</h4>
                <p v-if="user.species">
                  {{ user.species.name }} from {{ user.homeworld.name }}
                </p>
              </section>
            </RouterLink>
          </section>
        </section>
      </template>
    </ApolloQuery>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: "Home",
};
</script>
<style scoped>
.link-character {
  text-decoration: none;
}

</style>
