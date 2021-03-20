<template>
  <div class="detail">
    <!-- Filtrar apollo query -->
    <ApolloQuery
      :query="
        (gql) => gql`
          query MyHelloQuery($personId: ID) {
            person(id: $personId) {
              name
              birthYear
              eyeColor
              hairColor
              skinColor
              vehicleConnection {
                vehicles {
                  name
                }
              }
            }
          }
        `
      "
      :variables="{ personId }"
    >
      <template v-slot="{ result: { loading, error, data } }">
        <section v-if="loading">Loading...</section>
        <section v-else-if="error">An error occurred</section>
        <section v-else-if="data">
          <h2>{{ data.person.name }}</h2>
          <section>
            <h3>General Information</h3>
            <li v-if="data.person.eyeColor">
              Eye Color {{ data.person.eyeColor }}
            </li>
            <li v-if="data.person.hairColor">
              Hair Color{{ data.person.hairColor }}
            </li>
            <li v-if="data.person.skinColor">
              Skin Color{{ data.person.skinColor }}
            </li>
            <li v-if="data.person.birthYear">
              Birth Year{{ data.person.birthYear }}
            </li>
          </section>
          <section>
            <h3>Vehicles</h3>
            <section v-for="vehicle in data.person.vehicleConnection.vehicles" :key="vehicle.id">
              <li>{{vehicle.name}}</li>
            </section>
          </section>
        </section>
      </template>
    </ApolloQuery>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: "Detail",
  props: ["personId"],
};
</script>
<style scoped></style>
