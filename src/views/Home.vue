<template>
  <div class="home">
    <header>
      People of Star Wars
    </header>
    <!-- <font-awesome-icon :icon="['fas', 'robot']"/> -->
    <ApolloQuery :query="require('../graphql/allUsers.gql')">
      <template v-slot="{ result: { loading, error, data } }">
        <section v-if="loading" class="loading apollo">
          ...Loading
        </section>
        <section v-else-if="error" class="error apollo">
          An error occurred
        </section>
        <section v-else-if="data" class="result apollo">
          <section v-for="user in data.allPeople.people" :key="user.id">
            <RouterLink :to="`character/${user.id}`" class="link-character">
              <section class="container-character">
                <section>
                  <h4>{{ user.name }}</h4>
                  <section class="container-description">
                    <p>
                      <span v-if="user.species"
                        >{{ user.species.name }} from &nbsp;</span
                      >
                      <span v-if="user.homeworld"
                        >&nbsp; {{ user.homeworld.name }}</span
                      >
                    </p>
                  </section>
                </section>
                <i class="fas fa-angle-right"></i>
              </section>
            </RouterLink>
          </section>
        </section>
        <div v-else class="no-result apollo">
          <LoadSpinner></LoadSpinner>
        </div>
      </template>
    </ApolloQuery>
  </div>
</template>

<script>
// @ is an alias to /src

import LoadSpinner from "../components/LoadSpinner.vue";
export default {
  components: { LoadSpinner },
  name: "Home",
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
  justify-content: center;
  align-items: center;
}

h4 {
  font-style: normal;
  font-weight: bold;
  font-size: 17px;
  line-height: 20px;
  display: flex;
  align-items: center;
  letter-spacing: 0.0125em;
  color: #333333;
}

.container-character {
  height: 69px;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  padding: 16px;
  display: flex;
  justify-content: space-between;
}

.container-character i{
  color:#333333;
}
.container-description {
  font-weight: normal;
  font-size: 14px;
  line-height: 17px;
  display: flex;
  align-items: center;
  letter-spacing: 0.0125em;
  color: #828282;
}

.link-character {
  text-decoration: none;
}
</style>
