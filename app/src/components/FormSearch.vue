<template>
  <form ref="form" :style="style" @submit.prevent="$emit('fetch-user')">
    <div class="search-container">
      <img src="@/assets/icons/search.svg" alt="" />
      <input
        type="text"
        placeholder="Digite um nome de usuário"
        required
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
      />
    </div>
    <button>
      <img src="@/assets/icons/github.svg" alt="" />
      Buscar
    </button>
  </form>
</template>

<script setup>
import { ref, computed } from "vue";

const props = defineProps(["modelValue", "dataUser", "userNotFound"]);
const emits = defineEmits(["eventFetchUser", "update:modelValue"]);

const style = computed(() => {
  if (props.userNotFound) {
    return {
      border: "1px solid #b31d1d",
      boxShadow: "0px 0px 5px #eebbbb",
    };
  }
});
</script>

<style scoped lang="scss">
@import "../scss/abstracts/mixins.scss";

form {
  display: grid;
  grid-template-columns: 1fr auto;
  gap: 5px;
  width: 100%;
  background: #fff;
  border: 1px solid transparent;
  border-radius: 12px;
  box-shadow: 0px 0px 10px #cbcfe4;
  padding: 10px;
  transition: 0.5s;

  @include responsive("medium") {
    margin-top: 100px;
  }

  .search-container {
    display: flex;
    align-items: center;
    gap: 10px;

    img {
      margin-left: 5px;
    }

    input {
      font-family: "Inter", sans-serif;
      font-size: 1rem;
      letter-spacing: -0.5px;
      color: #222;
      width: 100%;
      &::placeholder {
        color: #bbb;
      }
    }
  }

  button {
    display: flex;
    align-items: center;
    gap: 8px;
    background: #6f768d;
    font-family: "Inter", sans-serif;
    letter-spacing: -0.5px;
    color: #fff;
    border-radius: 8px;
    padding: 8px 16px;
    cursor: pointer;
    transition: 0.5s;
    &:hover {
      box-shadow: 0px 3px 10px #9da3c0;
    }
  }
}
</style>
