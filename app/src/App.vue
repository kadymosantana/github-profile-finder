<template>
  <FormSearch
    @event-fetch-user="fetchUser"
    v-model="searchValue"
    :dataUser="dataUser"
    :userNotFound="userNotFound"
  />
  <InfosUser :dataUser="dataUser" />
</template>

<script>
import { ref } from "vue";
import FormSearch from "@/components/FormSearch.vue";
import InfosUser from "@/components/InfosUser.vue";

export default {
  name: "App",
  components: {
    FormSearch,
    InfosUser,
  },

  setup() {
    const dataUser = ref(null);
    const userNotFound = ref(null);
    const searchValue = ref("");

    function fetchUser() {
      fetch(`https://api.github.com/users/${searchValue.value}`)
        .then((r) => r.json())
        .then((r) => {
          if (!r.message) {
            dataUser.value = r;
            userNotFound.value = null;
            searchValue.value = "";
          } else {
            userNotFound.value = r;
          }
        });
    }

    return {
      dataUser,
      userNotFound,
      searchValue,
      fetchUser,
    };
  },
};
</script>

<style lang="scss">
@import "./scss/abstracts/mixins.scss";
@import "./scss/base/reset.scss";

#app {
  display: flex;
  flex-direction: column;
  gap: 20px;
  max-width: 100vw;
  @include responsive("medium") {
    max-width: max-content;
    padding: 30px;
  }
}
</style>
