<template>
  <div class="detail">
    <p>character id {{ person }}</p>
    <!-- Filtrar apollo query -->
    <ApolloQuery
      :query="
        (gql) => gql`
          query MyHelloQuery($person: ID) {
            person(id: $person) {
              name
              birthYear
              gender
              species {
                name
              }
            }
          }
        `
      "
      :variables="{ person }"
    >
      <template v-slot="{ result: { loading, error, data } }">
        <section v-if="loading">Loading...</section>
        <section v-else-if="error">An error occurred</section>
        <section v-else-if="data">
          {{ data.person }}
          
        </section>
      </template>
    </ApolloQuery>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: "Detail",
  props: ["person"],
};
</script>
<style scoped></style>
