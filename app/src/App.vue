<template>
  <FormSearch
    @event-fetch-user="fetchUser"
    v-model="searchValue"
    :dataUser="dataUser"
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
    const searchValue = ref("");

    function fetchUser() {
      fetch(`https://api.github.com/users/${searchValue.value}`)
        .then((r) => r.json())
        .then((r) => (dataUser.value = r));
      searchValue.value = "";
    }

    return {
      dataUser,
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

body {
  display: grid;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background: #f1f4ff;
  font-family: "Inter", sans-serif;
  color: #222;
  letter-spacing: -0.5px;
}
</style>
