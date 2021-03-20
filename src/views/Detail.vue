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
          <header>
            <router-link class="link-company" :to="'/'"
              >
            <i class="fas fa-arrow-left"></i>
            </router-link>
            <section>
               <h2>{{ data.person.name }}</h2>
            </section>
          </header>
          <section>
            <section class="title-section">
              <h3>General Information</h3>
            </section>
            <section class="item" v-if="data.person.eyeColor">
              <div class="title-item">Eye Color</div>
              <div class="data-item">{{ data.person.eyeColor }}</div>
            </section>
            <section class="item" v-if="data.person.hairColor">
              <div class="title-item">Hair Color</div>
              <div class="data-item">{{ data.person.hairColor }}</div>
            </section>
            <section class="item" v-if="data.person.skinColor">
              <div class="title-item">Skin Color</div> 
              <div class="data-item">{{ data.person.skinColor }}</div> 
            </section>
            <section class="item" v-if="data.person.birthYear">
              <div class="title-item">Birth Year</div>
              <div class="data-item">{{ data.person.birthYear }}</div>
            </section>
          </section>
          <section>
            <section class="title-section">
              <h3>Vehicles</h3>
            </section>
            <section v-for="vehicle in data.person.vehicleConnection.vehicles" :key="vehicle.id">
              <section class="item" >
                <div class="title-item">{{vehicle.name}}</div>
              </section>
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
<style scoped>
header {
  height: 53px;
  background-color: #121212;
  color: #ffffff;
  font-weight: bold;
  font-size: 17px;
  line-height: 20px;
  display: flex;
  letter-spacing: 0.0125em;
  align-items: center;
  padding: 0 23px;
}

header .fa-arrow-left{
 color: #ffffff;
}

header section{
  width: 90%;
  display: flex;
  justify-content: center;
}
h2{
font-weight: bold;
  font-size: 17px;
  line-height: 20px;
  letter-spacing: 0.0125em;
}

.title-section{
  height: 60px;
  padding: 32px 0 8px 16px;
}

h3{
font-style: normal;
font-weight: bold;
font-size: 17px;
line-height: 20px;
color: #333333;
}

.item{
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  height: 49px;
  display: flex;
  padding: 0 16px 0 16px;
  align-items: center;
  justify-content: space-between;
  font-weight: bold;
}

.title-item{
  color:#828282;
}

</style>
