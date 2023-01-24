<template>
  <FormSearch
    @fetch-user="fetchUser"
    v-model="searchValue"
    :dataUser="dataUser"
    :userNotFound="userNotFound"
  />
  <Transition mode="out-in">
    <InfosUser v-if="dataUser?.id" :dataUser="dataUser" />
  </Transition>
</template>

<script setup>
import { ref } from "vue";
import FormSearch from "@/components/FormSearch.vue";
import InfosUser from "@/components/InfosUser.vue";

const dataUser = ref(null);
const userNotFound = ref(null);
const searchValue = ref("");

const fetchUser = () => {
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

.v-enter-from,
.v-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}

.v-enter-active,
.v-leave-active {
  transition: 0.3s;
}
</style>
